---
title: Chiamata  AEM Forms tramite JavaAPI
seo-title: Chiamata  AEM Forms tramite JavaAPI
description: Utilizzare l'API Java di AEM Forms  per il protocollo di trasporto RMI per la chiamata remota, il trasporto VM per la chiamata locale, SOAP per la chiamata remota, autenticazione diversa, come nome utente e password, e richieste di chiamata sincrone e asincrone.
seo-description: Utilizzare l'API Java di AEM Forms  per il protocollo di trasporto RMI per la chiamata remota, il trasporto VM per la chiamata locale, SOAP per la chiamata remota, autenticazione diversa, come nome utente e password, e richieste di chiamata sincrone e asincrone.
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '5494'
ht-degree: 0%

---


# Chiamata  AEM Forms mediante l&#39;API Java {#invoking-aem-forms-using-the-javaapi}

**Esempi ed esempi in questo documento sono disponibili solo per  AEM Forms nell&#39;ambiente JEE.**

 AEM Forms può essere invocato utilizzando l&#39;API Java  AEM Forms. Quando utilizzate l&#39;API Java di AEM Forms , potete utilizzare l&#39;API di vocazione o le librerie client Java. Le librerie client Java sono disponibili per servizi come il servizio di Rights Management. Queste API fortemente tipizzate consentono di sviluppare applicazioni Java che richiamano  AEM Forms.

L&#39;API Invocation è una classe che si trova nel pacchetto `com.adobe.idp.dsc`. Utilizzando queste classi, potete inviare una richiesta di chiamata direttamente a un servizio e gestire una risposta di chiamata restituita. Utilizzare l&#39;API Invocation per richiamare i processi di breve durata o di lunga durata creati utilizzando Workbench.

Il metodo consigliato per richiamare un servizio a livello di programmazione consiste nell&#39;utilizzare una libreria client Java corrispondente al servizio anziché l&#39;API di vocazione. Ad esempio, per richiamare il servizio di cifratura, utilizzate la libreria client del servizio di cifratura. Per eseguire un&#39;operazione del servizio di cifratura, richiamare un metodo che appartiene all&#39;oggetto client del servizio di cifratura. È possibile cifrare un documento PDF con una password richiamando il metodo `EncryptionServiceClient` dell&#39;oggetto `encryptPDFUsingPassword`.

L&#39;API Java supporta le seguenti funzionalità:

* Protocollo di trasporto RMI per chiamata remota
* Trasporto VM per invocazione locale
* SOAP per chiamata remota
* Autenticazione diversa, ad esempio nome utente e password
* Richieste di chiamata sincrone e asincrone

**Sito Web  Adobe per sviluppatori**

Il sito Web  Adobe Developer contiene i seguenti articoli che discutono della chiamata  servizi AEM Forms mediante l&#39;API Java:

[Utilizzo di servlet Java per richiamare  processi AEM Forms](https://www.adobe.com/devnet/livecycle/articles/java_servlets.html)

[Richiamo dell&#39;API Distiller di  da Java](https://www.adobe.com/devnet/livecycle/articles/distiller_java_03.html)

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](#including-aem-forms-java-library-files)

[Richiamo di processi a lunga durata basati sull&#39;uomo](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Chiamata  AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Impostazione delle proprietà di connessione](#setting-connection-properties)

[Trasmissione di dati a  servizi AEM Forms tramite Java API](#passing-data-to-aem-forms-services-using-the-java-api)

[Chiamata di un servizio tramite una libreria client Java](#invoking-a-service-using-a-java-client-library)

[Richiamo di un processo di breve durata tramite l&#39;API di incitamento](#invoking-a-short-lived-process-using-the-invocation-api)

[Creazione di un&#39;applicazione Web Java che richiama un processo longevo incentrato sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md)

## Inclusione  file libreria Java AEM Forms {#including-aem-forms-java-library-files}

Per richiamare un servizio AEM Forms  a livello di programmazione utilizzando l&#39;API Java, includete i file libreria richiesti (file JAR) nel percorso di classe del progetto Java. I file JAR inclusi nel percorso di classe dell&#39;applicazione client dipendono da diversi fattori:

* Il servizio AEM Forms  da richiamare. Un&#39;applicazione client può richiamare uno o più servizi.
* Modalità in cui si desidera richiamare un servizio AEM Forms . È possibile utilizzare la modalità EJB o SOAP. (Vedere [Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Solo chiavi in mano) Avviare il server AEM Forms  con il comando `standalone.bat -b <Server IP> -c lc_turnkey.xml` per specificare un IP server per EJB

* Il server applicazione J2EE su cui è distribuito  AEM Forms.

### File JAR specifici del servizio {#service-specific-jar-files}

Nella tabella seguente sono elencati i file JAR necessari per richiamare  servizi AEM Forms.

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
   <td><p>Deve essere sempre incluso nel percorso di classe di un'applicazione client Java.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Deve essere sempre incluso nel percorso di classe di un'applicazione client Java.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Deve essere sempre incluso nel percorso di classe di un'applicazione client Java.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk//client-libs/&lt;app server=""&gt;<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Application Manager.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Assembler. </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Richiesto per richiamare l'API del servizio Backup e ripristino.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio moduli con codice a barre. </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Converti PDF. </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Distiller.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio DocConverter.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Document Management.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio di cifratura.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Forms.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio di integrazione dei dati del modulo.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Generate PDF.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Genera PDF 3D.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Job Manager. </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Output.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Utilità PDF o Utilità XMP.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio di estensione Acrobat Reader DC.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Repository.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs\thirdparty<i></i></p></td>
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
   <td><p>Obbligatorio per richiamare il servizio Rights Management.</p><p>Se  AEM Forms è distribuito su JBoss, includete tutti questi file. </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p><p>Directory lib specifica per JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Signature.</p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Task Manager. </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Archivio attendibili. </p></td>
   <td><p>&lt;&gt;install directory</i>&gt;/sdk/client-libs/common<i></i></p></td>
  </tr>
 </tbody>
</table>

### Modalità di connessione e file JAR dell&#39;applicazione J2EE {#connection-mode-and-j2ee-application-jar-files}

Nella tabella seguente sono elencati i file JAR che dipendono dalla modalità di connessione e dal server applicazione J2EE su cui  AEM Forms è distribuito.

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
   <td><p>se  AEM Forms viene richiamato utilizzando la modalità SOAP, includete questi file JAR.</p> </td>
   <td><p>&lt;&gt;install directory</em>&gt;/sdk/client-libs/third-party<em></em></p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>se  AEM Forms è distribuito su JBoss Application Server, includete questo file JAR.</p> <p>Le classi obbligatorie non vengono trovate dal caricatore di classe se jboss-client.jar e le barre di riferimento non sono co-posizionate.</p> </td>
   <td><p>Directory lib client JBoss</p> <p>Se distribuite l’applicazione client sullo stesso server applicazione J2EE, non è necessario includere questo file.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>se  AEM Forms è distribuito su BEA WebLogic Server®, includete questo file JAR.</p> </td>
   <td><p>Directory lib specifica per WebLogic</p> <p>Se distribuite l’applicazione client sullo stesso server applicazione J2EE, non è necessario includere questo file.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>se  AEM Forms è distribuito su WebSphere Application Server, includete questi file JAR.</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar è richiesto per la chiamata al servizio Web).</p> </li>
    </ul> </td>
   <td><p>Directory lib specifica per WebSphere (<em>[WAS_HOME]</em>/runtime)</p> <p>Se distribuite l’applicazione client sullo stesso server applicazione J2EE, non è necessario includere tali file.</p> </td>
  </tr>
 </tbody>
</table>

### Richiamo di scenari {#invoking-scenarios}

La tabella seguente specifica gli scenari di chiamata ed elenca i file JAR richiesti per richiamare  AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Servizi</p> </th>
   <th><p>Modalità di incitamento</p> </th>
   <th><p>Server applicazioni J2EE</p> </th>
   <th><p>File JAR richiesti</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>servizio Forms</p> </td>
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
   <td><p>servizio Forms</p> <p>Servizio estensioni Acrobat Reader DC</p> <p>Servizio Firma</p> </td>
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
   <td><p>servizio Forms</p> </td>
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
   <td><p>servizio Forms</p> <p>Servizio estensioni Acrobat Reader DC</p> <p>Servizio Firma</p> </td>
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

Se state effettuando l&#39;aggiornamento da LiveCycle a  AEM Forms, si consiglia di includere i file  AEM Forms JAR nel percorso di classe del progetto Java. Ad esempio, se utilizzate servizi come il servizio di Rights Management, si verificherà un problema di compatibilità se non includete  file AEM Forms JAR nel percorso di classe.

Presupponendo che si stia effettuando l&#39;aggiornamento a  AEM Forms. Per utilizzare un&#39;applicazione Java che richiama il servizio di Rights Management, includete le versioni AEM Forms  dei seguenti file JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulta anche**

[Chiamata  AEM Forms tramite l&#39;API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

[Trasmissione di dati a  servizi AEM Forms tramite Java API](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Chiamata di un servizio tramite una libreria client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Impostazione delle proprietà di connessione {#setting-connection-properties}

Le proprietà di connessione vengono impostate per richiamare  AEM Forms quando si utilizza l&#39;API Java. Quando si impostano le proprietà di connessione, specificare se richiamare i servizi in remoto o in locale, nonché la modalità di connessione e i valori di autenticazione. I valori di autenticazione sono obbligatori se è abilitata la protezione del servizio. Tuttavia, se la protezione del servizio è disabilitata, non è necessario specificare i valori di autenticazione.

La modalità di connessione può essere SOAP o EJB. La modalità EJB utilizza il protocollo RMI/IIOP e le prestazioni della modalità EJB sono migliori delle prestazioni della modalità SOAP. La modalità SOAP viene utilizzata per eliminare una dipendenza del server applicazione J2EE o quando si trova un firewall tra  AEM Forms e l&#39;applicazione client. La modalità SOAP utilizza il protocollo https come trasporto sottostante e può comunicare attraverso i confini del firewall. Se non esiste una dipendenza da un server applicazione J2EE o un firewall, si consiglia di utilizzare la modalità EJB.

Per richiamare un servizio AEM Forms , impostate le seguenti proprietà di connessione:

* **DSC_DEFAULT_EJB_ENDPOINT:** Se utilizzate la modalità di connessione EJB, questo valore rappresenta l&#39;URL del server applicazione J2EE su cui  AEM Forms è distribuito. Per richiamare  AEM Forms in remoto, specificate il nome del server applicazione J2EE sul quale &#39;AEM Forms è distribuito. Se l&#39;applicazione client si trova sullo stesso server applicazione J2EE, è possibile specificare `localhost`. A seconda del server applicazioni J2EE  AEM Forms è distribuito, specificate uno dei seguenti valori:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Se si utilizza la modalità di connessione SOAP, questo valore rappresenta l&#39;endpoint a cui viene inviata una richiesta di chiamata. Per richiamare  AEM Forms in remoto, specificate il nome del server applicazione J2EE sul quale &#39;AEM Forms è distribuito. Se l&#39;applicazione client si trova sullo stesso server applicazione J2EE, è possibile specificare `localhost` (ad esempio, `http://localhost:8080`).

   * Il valore della porta `8080` è applicabile se l&#39;applicazione J2EE è JBoss. Se il server applicazioni J2EE è IBM® WebSphere®, utilizzare la porta `9080`. Analogamente, se il server applicazione J2EE è WebLogic, utilizzare la porta `7001`. (Questi valori sono valori di porta predefiniti. Se modificate il valore della porta, utilizzate il numero di porta applicabile.

* **DSC_TRANSPORT_PROTOCOL**: Se si utilizza la modalità di connessione EJB, specificare  `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` per questo valore. Se si utilizza la modalità di connessione SOAP, specificare `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Specifica il server applicazioni J2EE su cui  AEM Forms è distribuito. I valori validi sono `JBoss`, `WebSphere`, `WebLogic`.

   * Se si imposta questa proprietà di connessione su `WebSphere`, il valore `java.naming.factory.initial` è impostato su `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Se si imposta questa proprietà di connessione su `WebLogic`, il valore `java.naming.factory.initial` è impostato su `weblogic.jndi.WLInitialContextFactory`.
   * Analogamente, se si imposta questa proprietà di connessione su `JBoss`, il valore `java.naming.factory.initial` viene impostato su `org.jnp.interfaces.NamingContextFactory`.
   * Se non si desidera utilizzare i valori predefiniti, è possibile impostare la proprietà `java.naming.factory.initial` su un valore che soddisfa i requisiti dell&#39;utente.

   >[!NOTE]
   >
   >Invece di utilizzare una stringa per impostare la proprietà di connessione `DSC_SERVER_TYPE`, è possibile utilizzare un membro statico della classe `ServiceClientFactoryProperties`. È possibile utilizzare i seguenti valori: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE` o `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** specifica il nome utente del modulo AEM. Affinché un utente possa richiamare correttamente un servizio AEM Forms , deve avere il ruolo Utente servizi. Un utente può anche avere un altro ruolo che include l&#39;autorizzazione Richiamo assistenza. In caso contrario, viene generata un&#39;eccezione quando tentano di richiamare un servizio. Se la protezione del servizio è disabilitata, non è necessario specificare questa proprietà di connessione.
* **DSC_CREDENTIAL_PASSWORD:** specifica il valore della password corrispondente. Se la protezione del servizio è disabilitata, non è necessario specificare questa proprietà di connessione.
* **DSC_REQUEST_TIMEOUT:** il limite di timeout della richiesta predefinita per la richiesta SOAP è di 1200000 millisecondi (20 minuti). A volte, una richiesta può richiedere più tempo per completare l&#39;operazione. Ad esempio, una richiesta SOAP che recupera un insieme di record di grandi dimensioni può richiedere un limite di timeout più lungo. È possibile utilizzare `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` per aumentare il limite di timeout delle chiamate per le richieste SOAP.

   **nota**: Solo le chiamate basate su SOAP supportano la proprietà DSC_REQUEST_TIMEOUT.

Per impostare le proprietà di connessione, eseguire le operazioni seguenti:

1. Creare un oggetto `java.util.Properties` utilizzando il relativo costruttore.
1. Per impostare la proprietà di connessione `DSC_DEFAULT_EJB_ENDPOINT`, richiamare il metodo `java.util.Properties` dell&#39;oggetto `setProperty` e passare i seguenti valori:

   * Il valore di enumerazione `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`
   * Una stringa che specifica l&#39;URL del server applicazione J2EE che ospita  AEM Forms

   >[!NOTE]
   >
   >Se si utilizza la modalità di connessione SOAP, specificare il valore di enumerazione `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` invece del valore di enumerazione `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`.

1. Per impostare la proprietà di connessione `DSC_TRANSPORT_PROTOCOL`, richiamare il metodo `java.util.Properties` dell&#39;oggetto `setProperty` e passare i seguenti valori:

   * Il valore di enumerazione `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL`
   * Il valore di enumerazione `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`

   >[!NOTE]
   >
   >Se si utilizza la modalità di connessione SOAP, specificare il valore di enumerazione `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`invece del valore di enumerazione `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`.

1. Per impostare la proprietà di connessione `DSC_SERVER_TYPE`, richiamare il metodo `java.util.Properties` dell&#39;oggetto `setProperty` e passare i seguenti valori:

   * Il valore di enumerazione `ServiceClientFactoryProperties.DSC_SERVER_TYPE`
   * Un valore di stringa che specifica il server applicazione J2EE che ospita  AEM Forms (ad esempio, se  AEM Forms è distribuito su JBoss, specificare `JBoss`).

      1. Per impostare la proprietà di connessione `DSC_CREDENTIAL_USERNAME`, richiamare il metodo `java.util.Properties` dell&#39;oggetto `setProperty` e passare i seguenti valori:
   * Il valore di enumerazione `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME`
   * Una stringa che specifica il nome utente richiesto per richiamare  AEM Forms

      1. Per impostare la proprietà di connessione `DSC_CREDENTIAL_PASSWORD`, richiamare il metodo `java.util.Properties` dell&#39;oggetto `setProperty` e passare i seguenti valori:
   * Il valore di enumerazione `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD`
   * Valore stringa che specifica il valore della password corrispondente



**Impostazione della modalità di connessione EJB per JBoss**

L&#39;esempio di codice Java seguente imposta le proprietà di connessione per richiamare  AEM Forms distribuito su JBoss e utilizzare la modalità di connessione EJB.

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

L&#39;esempio di codice Java seguente imposta le proprietà di connessione per richiamare  AEM Forms distribuito su WebLogic e utilizzare la modalità di connessione EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Impostazione della modalità di connessione EJB per WebSphere**

L&#39;esempio di codice Java seguente imposta le proprietà di connessione per richiamare  AEM Forms distribuito su WebSphere e utilizzare la modalità di connessione EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Impostazione della modalità di connessione SOAP**

L&#39;esempio di codice Java seguente imposta le proprietà di connessione in modalità SOAP per richiamare  AEM Forms distribuito su JBoss.

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
>Se selezionate la modalità di connessione SOAP, accertatevi di includere ulteriori file JAR nel percorso di classe dell&#39;applicazione client.

**Impostazione delle proprietà di connessione quando la protezione del servizio è disabilitata**

L&#39;esempio di codice Java seguente imposta le proprietà di connessione necessarie per richiamare  AEM Forms distribuito su JBoss Application Server e quando la protezione del servizio è disabilitata.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Tutti gli avvii rapidi Java associati alla programmazione con  AEM Forms mostrano le impostazioni di connessione EJB e SOAP.

**Impostazione della modalità di connessione SOAP con il limite di timeout della richiesta personalizzata**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Utilizzo di un oggetto Context per richiamare  AEM Forms**

È possibile utilizzare un oggetto `com.adobe.idp.Context` per richiamare un servizio AEM Forms  con un utente autenticato (l&#39;oggetto `com.adobe.idp.Context` rappresenta un utente autenticato). Quando si utilizza un oggetto `com.adobe.idp.Context`, non è necessario impostare le proprietà `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD`. È possibile ottenere un oggetto `com.adobe.idp.Context` durante l&#39;autenticazione degli utenti utilizzando il metodo `AuthenticationManagerServiceClient` dell&#39;oggetto `authenticate`.

Il metodo `authenticate` restituisce un oggetto `AuthResult` che contiene i risultati dell&#39;autenticazione. È possibile creare un oggetto `com.adobe.idp.Context` richiamandone il costruttore. Quindi, richiamare il metodo `com.adobe.idp.Context` dell&#39;oggetto `initPrincipal` e passare l&#39;oggetto `AuthResult`, come illustrato nel codice seguente:

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

Anziché impostare le proprietà `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD`, è possibile richiamare il metodo `ServiceClientFactory` dell&#39;oggetto `setContext` e passare l&#39;oggetto `com.adobe.idp.Context`. Quando si utilizza un utente di moduli AEM per richiamare un servizio, assicurarsi di avere il ruolo `Services User` richiesto per richiamare un servizio AEM Forms .

L&#39;esempio di codice seguente mostra come utilizzare un oggetto `com.adobe.idp.Context` all&#39;interno delle impostazioni di connessione, utilizzato per creare un oggetto `EncryptionServiceClient`.

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
>Per informazioni complete sull&#39;autenticazione di un utente, vedere [Autenticazione di utenti](/help/forms/developing/users.md#authenticating-users).

### Richiamo di scenari {#invoking_scenarios-1}

In questa sezione vengono descritti i seguenti scenari di richiamo:

* Un&#39;applicazione client in esecuzione nella propria macchina virtuale Java (JVM) richiama un&#39;istanza autonoma  AEM Forms.
* Un&#39;applicazione client in esecuzione nel proprio JVM richiama istanze AEM Forms  cluster.

### Applicazione client che richiama un&#39;istanza autonoma  AEM Forms {#client-application-invoking-a-stand-alone-aem-forms-instance}

Il diagramma seguente mostra un&#39;applicazione client in esecuzione nella propria JVM e che richiama un&#39;istanza autonoma  AEM Forms.

In questo scenario, un&#39;applicazione client è in esecuzione in una propria JVM e richiama  servizi AEM Forms.

>[!NOTE]
>
>Questo scenario è lo scenario di richiamo su cui si basano tutti gli avvii rapidi.

### Applicazione client che richiama istanze AEM Forms  cluster {#client-application-invoking-clustered-aem-forms-instances}

Il diagramma seguente mostra un&#39;applicazione client in esecuzione nella propria JVM e che richiama  istanze AEM Forms presenti in un cluster.

Questo scenario è simile a quello di un&#39;applicazione client che richiama un&#39;istanza autonoma  AEM Forms. Tuttavia, l&#39;URL del fornitore è diverso. Se un&#39;applicazione client desidera connettersi a un server applicazione J2EE specifico, l&#39;applicazione deve modificare l&#39;URL per fare riferimento al server applicazione J2EE specifico.

Non è consigliabile fare riferimento a uno specifico server applicazione J2EE perché la connessione tra l&#39;applicazione client e  AEM Forms viene terminata se il server applicazioni si arresta. È consigliabile che l&#39;URL del provider faccia riferimento a un gestore JNDI a livello di cella, invece di un server applicazione J2EE specifico.

Le applicazioni client che utilizzano la modalità di connessione SOAP possono utilizzare la porta di bilanciamento del carico HTTP per il cluster. Le applicazioni client che utilizzano la modalità di connessione EJB possono connettersi alla porta EJB di un server applicazione J2EE specifico. Questa azione gestisce il bilanciamento del carico tra i nodi del cluster.

**WebSphere**

L&#39;esempio seguente mostra il contenuto di un file jndi.properties utilizzato per connettersi a  AEM Forms distribuito su WebSphere.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

L&#39;esempio seguente mostra il contenuto di un file jndi.properties utilizzato per connettersi a  AEM Forms distribuito su WebLogic.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

L&#39;esempio seguente mostra il contenuto di un file jndi.properties utilizzato per connettersi a  AEM Forms distribuito su JBoss.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Consultate l’amministratore per determinare il nome del server applicazione J2EE e il numero di porta.

**Consulta anche**

[Inclusione  file libreria Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Trasmissione di dati a  servizi AEM Forms tramite Java API](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Chiamata di un servizio tramite una libreria client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Trasmissione di dati a  servizi AEM Forms tramite Java API {#passing-data-to-aem-forms-services-using-the-java-api}

 le operazioni del servizio AEM Forms in genere consumano o producono documenti PDF. Quando si richiama un servizio, talvolta è necessario trasmettere al servizio un documento PDF (o altri tipi di documento, come i dati XML). Analogamente, talvolta è necessario gestire un documento PDF restituito dal servizio. La classe Java che consente di trasmettere dati a e da  servizi AEM Forms è `com.adobe.idp.Document`.

 servizi AEM Forms non accettano un documento PDF come altri tipi di dati, ad esempio un oggetto `java.io.InputStream` o un array di byte. Un oggetto `com.adobe.idp.Document` può essere utilizzato anche per trasmettere ai servizi altri tipi di dati, come i dati XML.

Un oggetto `com.adobe.idp.Document` è un tipo serializzabile Java e può quindi essere trasmesso su una chiamata RMI. Il lato ricevente può essere collocato (stesso host, stesso loader di classe), locale (stesso host, diverso loader di classe) o remoto (host diverso). La trasmissione del contenuto del documento è ottimizzata per ogni caso. Ad esempio, se il mittente e il destinatario si trovano sullo stesso host, il contenuto viene trasmesso su un file system locale. In alcuni casi, i documenti possono essere passati in memoria.

A seconda delle dimensioni dell&#39;oggetto `com.adobe.idp.Document`, i dati vengono memorizzati all&#39;interno dell&#39;oggetto `com.adobe.idp.Document` o nel file system del server. Tutte le risorse di memorizzazione temporanea occupate dall&#39;oggetto `com.adobe.idp.Document` vengono rimosse automaticamente al momento dello smaltimento `com.adobe.idp.Document`. (Vedere [Eliminazione di oggetti documento](invoking-aem-forms-using-java.md#disposing-document-objects).)

A volte è necessario conoscere il tipo di contenuto di un oggetto `com.adobe.idp.Document` prima di trasmetterlo a un servizio. Ad esempio, se un&#39;operazione richiede un tipo di contenuto specifico, come `application/pdf`, è consigliabile determinare il tipo di contenuto. (Vedere [Definizione del tipo di contenuto di un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

L&#39;oggetto `com.adobe.idp.Document` tenta di determinare il tipo di contenuto utilizzando i dati forniti. Se il tipo di contenuto non può essere recuperato dai dati forniti (ad esempio, quando i dati sono stati forniti come array di byte), impostare il tipo di contenuto. Per impostare il tipo di contenuto, richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `setContentType`. (Vedere [Definizione del tipo di contenuto di un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Se i file collaterali risiedono sullo stesso file system, la creazione di un oggetto `com.adobe.idp.Document` è più rapida. Se i file collaterali risiedono su file system remoti, è necessario eseguire un&#39;operazione di copia, che influisce sulle prestazioni.

Un&#39;applicazione può contenere sia tipi di dati `com.adobe.idp.Document` che `org.w3c.dom.Document`. Tuttavia, accertati di qualificare completamente il tipo di dati `org.w3c.dom.Document`. Per informazioni sulla conversione di un oggetto `org.w3c.dom.Document` in un oggetto `com.adobe.idp.Document`, vedere [Avvio rapido (modalità EJB): Precompilazione di Forms con layout scorrevoli mediante l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>Per evitare una perdita di memoria in WebLogic durante l&#39;utilizzo di un oggetto `com.adobe.idp.Document`, leggere le informazioni del documento in blocchi di almeno 2048 byte. Ad esempio, il codice seguente legge le informazioni del documento in blocchi di 2048 byte:

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

[Chiamata  AEM Forms tramite l&#39;API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di documenti {#creating-documents}

Creare un oggetto `com.adobe.idp.Document` prima di richiamare un&#39;operazione di servizio che richiede un documento PDF (o altri tipi di documento) come valore di input. La classe `com.adobe.idp.Document` fornisce costruttori che consentono di creare un documento dai seguenti tipi di contenuto:

* Array a byte
* Un oggetto `com.adobe.idp.Document` esistente
* Oggetto `java.io.File`
* Oggetto `java.io.InputStream`
* Oggetto `java.net.URL`

#### Creazione di un documento basato su un array di byte {#creating-a-document-based-on-a-byte-array}

Nell&#39;esempio di codice seguente viene creato un oggetto `com.adobe.idp.Document` basato su un array di byte.

**Creazione di un oggetto Document basato su un array di byte**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### Creazione di un documento basato su un altro documento {#creating-a-document-based-on-another-document}

Nell&#39;esempio di codice seguente viene creato un oggetto `com.adobe.idp.Document` basato su un altro oggetto `com.adobe.idp.Document`.

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

Nell&#39;esempio di codice seguente viene creato un oggetto `com.adobe.idp.Document` basato su un file PDF denominato *map.pdf*. Questo file si trova nella radice del disco rigido C. Questo costruttore tenta di impostare il tipo di contenuto MIME dell&#39;oggetto `com.adobe.idp.Document` utilizzando l&#39;estensione del nome file.

Il costruttore `com.adobe.idp.Document` che accetta un oggetto `java.io.File` accetta anche un parametro booleano. Impostando questo parametro su `true`, l&#39;oggetto `com.adobe.idp.Document` elimina il file. Questo significa che non è necessario rimuovere il file dopo averlo passato al costruttore `com.adobe.idp.Document`.

Impostando questo parametro su `false` si mantiene la proprietà del file. L&#39;impostazione di questo parametro su `true` è più efficiente. Il motivo è che l&#39;oggetto `com.adobe.idp.Document` può spostare il file direttamente nell&#39;area gestita locale invece di copiarlo (il che è più lento).

**Creazione di un oggetto Document basato su un file PDF**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Creazione di un documento basato su un oggetto InputStream {#creating-a-document-based-on-an-inputstream-object}

Nell&#39;esempio di codice Java riportato di seguito viene creato un oggetto `com.adobe.idp.Document` basato su un oggetto `java.io.InputStream`.

**Creazione di un documento basato su un oggetto InputStream**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Creazione di un documento basato su contenuto accessibile da un URL {#creating-a-document-based-on-content-accessible-from-an-url}

Nell&#39;esempio di codice Java riportato di seguito viene creato un oggetto `com.adobe.idp.Document` basato su un file PDF denominato *map.pdf*. Questo file si trova all&#39;interno di un&#39;applicazione Web denominata `WebApp` in esecuzione su `localhost`. Questo costruttore tenta di impostare il tipo di contenuto MIME dell&#39;oggetto `com.adobe.idp.Document` utilizzando il tipo di contenuto restituito con il protocollo URL.

L&#39;URL fornito all&#39;oggetto `com.adobe.idp.Document` viene sempre letto sul lato in cui viene creato l&#39;oggetto `com.adobe.idp.Document` originale, come illustrato nell&#39;esempio seguente:

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

Il file c:/temp/input.pdf deve trovarsi sul computer client (non sul computer server). Nel computer client viene letto l&#39;URL e viene creato l&#39;oggetto `com.adobe.idp.Document`.

**Creazione di un documento basato su contenuto accessibile da un URL**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulta anche**

[Chiamata  AEM Forms tramite l&#39;API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestione dei documenti restituiti {#handling-returned-documents}

Le operazioni di servizio che restituiscono un documento PDF (o altri tipi di dati come i dati XML) come valore di output restituiscono un oggetto `com.adobe.idp.Document`. Dopo aver ricevuto un oggetto `com.adobe.idp.Document`, è possibile convertirlo nei seguenti formati:

* Oggetto `java.io.File`
* Oggetto `java.io.InputStream`
* Array a byte

La riga di codice seguente converte un oggetto `com.adobe.idp.Document` in un oggetto `java.io.InputStream`. Si supponga che `myPDFDocument` rappresenti un oggetto `com.adobe.idp.Document`:

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Allo stesso modo, potete copiare il contenuto di un `com.adobe.idp.Document` in un file locale eseguendo le seguenti operazioni:

1. Creare un oggetto `java.io.File`.
1. Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` e passare l&#39;oggetto `java.io.File`.

Nell&#39;esempio di codice seguente il contenuto di un oggetto `com.adobe.idp.Document` viene copiato in un file denominato *OtherMap.pdf*.

**Copia del contenuto di un oggetto documento in un file**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulta anche**

[Chiamata  AEM Forms tramite l&#39;API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinazione del tipo di contenuto di un documento {#determining-the-content-type-of-a-document}

Determinare il tipo MIME di un oggetto `com.adobe.idp.Document` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getContentType`. Questo metodo restituisce un valore di stringa che specifica il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`. La tabella seguente descrive i diversi tipi di contenuto restituiti da AEM Forms .

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
   <td><p>XML Data Packaging (XDP), utilizzato per i moduli XFA (XML Forms Architecture) esportati</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Segnalibri, allegati o altri documenti XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Forms Data Format (FDF), utilizzato per i moduli Acrobat esportati </p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML Forms Data Format (XFDF), utilizzato per i moduli Acrobat esportati </p></td>
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

L&#39;esempio di codice seguente determina il tipo di contenuto di un oggetto `com.adobe.idp.Document`.

**Determinazione del tipo di contenuto di un oggetto Document**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulta anche**

[Chiamata  AEM Forms tramite l&#39;API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminazione degli oggetti documento {#disposing-document-objects}

Se non è più necessario un oggetto `Document`, è consigliabile eliminarlo richiamandone il metodo `dispose`. Ogni oggetto `Document` utilizza un descrittore di file e fino a 75 MB di spazio RAM sulla piattaforma host dell&#39;applicazione. Se un oggetto `Document` non viene eliminato, il processo di raccolta Java Garage lo dispone. Tuttavia, prima di procedere con lo smaltimento utilizzando il metodo `dispose`, è possibile liberare la memoria occupata dall&#39;oggetto `Document`.

**Consulta anche**

[Chiamata  AEM Forms tramite l&#39;API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Chiamata di un servizio tramite una libreria client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Chiamata di un servizio tramite una libreria client Java {#invoking-a-service-using-a-java-client-library}

 le operazioni del servizio AEM Forms possono essere invocate utilizzando l&#39;API fortemente tipizzata di un servizio, nota come libreria client Java. Una *libreria client Java* è un insieme di classi concrete che forniscono l&#39;accesso ai servizi distribuiti nel contenitore di servizi. È possibile creare un&#39;istanza di un oggetto Java che rappresenta il servizio da richiamare invece di creare un oggetto `InvocationRequest` utilizzando l&#39;API Invocation. L&#39;API Invocation viene utilizzata per richiamare i processi, ad esempio quelli di lunga durata, creati in Workbench. (Vedere [Richiamo di processi a lunga durata basati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Per eseguire un&#39;operazione di servizio, richiamare un metodo che appartiene all&#39;oggetto Java. Una libreria client Java contiene metodi che in genere associano uno a uno con le operazioni del servizio. Quando utilizzate una libreria client Java, impostate le proprietà di connessione richieste. (Vedere [Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties).)

Dopo aver impostato le proprietà di connessione, creare un oggetto `ServiceClientFactory` utilizzato per creare un&#39;istanza di un oggetto Java che consente di richiamare un servizio. Ogni servizio con una libreria client Java ha un oggetto client corrispondente. Ad esempio, per richiamare il servizio Repository, creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`. L&#39;oggetto `ServiceClientFactory` è responsabile della gestione delle impostazioni di connessione necessarie per richiamare  servizi AEM Forms.

Anche se ottenere un `ServiceClientFactory` è in genere veloce, alcuni sovraccarichi sono coinvolti quando la fabbrica viene utilizzata per la prima volta. Questo oggetto è ottimizzato per il riutilizzo e quindi, quando possibile, utilizza lo stesso oggetto `ServiceClientFactory` quando si creano più oggetti client Java. Ovvero, non creare un oggetto `ServiceClientFactory` separato per ciascun oggetto libreria client creato.

È presente un&#39;impostazione di User Manager che controlla la durata dell&#39;asserzione SAML all&#39;interno dell&#39;oggetto `com.adobe.idp.Context` che interessa l&#39;oggetto `ServiceClientFactory`. Questa impostazione controlla tutti i tempi di vita del contesto di autenticazione in  AEM Forms, incluse tutte le chiamate eseguite utilizzando l&#39;API Java. Per impostazione predefinita, il periodo di tempo in cui è possibile utilizzare un oggetto `ServiceCleintFactory` è di due ore.

>[!NOTE]
>
>Per spiegare come richiamare un servizio utilizzando l&#39;API Java, viene richiamata l&#39;operazione `writeResource` del servizio Repository. Questa operazione consente di inserire una nuova risorsa nella directory archivio.

È possibile richiamare il servizio Repository utilizzando una libreria client Java ed eseguendo i seguenti passaggi:

1. Includete file JAR client, ad esempio adobe-repository-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, vedere [Inclusione  file libreria Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Impostare le proprietà di connessione necessarie per richiamare un servizio.
1. Creare un oggetto `ServiceClientFactory` richiamando il metodo `ServiceClientFactory` statico dell&#39;oggetto `createInstance` e passando l&#39;oggetto `java.util.Properties` che contiene le proprietà di connessione.
1. Creare un oggetto `ResourceRepositoryClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`. Utilizzare l&#39;oggetto `ResourceRepositoryClient` per richiamare le operazioni del servizio Repository.
1. Creare un oggetto `RepositoryInfomodelFactoryBean` utilizzando il relativo costruttore e passare `null`. Questo oggetto consente di creare un oggetto `Resource` che rappresenta il contenuto aggiunto alla directory archivio.
1. Creare un oggetto `Resource` richiamando il metodo `RepositoryInfomodelFactoryBean` dell&#39;oggetto `newImage` e passando i seguenti valori:

   * Un valore ID univoco specificando `new Id()`.
   * Un valore UUID univoco specificando `new Lid()`.
   * Nome della risorsa. È possibile specificare il nome del file XDP.

   Inserite il valore restituito in `Resource`.

1. Creare un oggetto `ResourceContent` richiamando il metodo `RepositoryInfomodelFactoryBean` dell&#39;oggetto `newImage` e collocando il valore restituito su `ResourceContent`. Questo oggetto rappresenta il contenuto aggiunto alla directory archivio.
1. Creare un oggetto `com.adobe.idp.Document` passando un oggetto `java.io.FileInputStream` che memorizza il file XDP da aggiungere alla directory archivio. Vedere [Creazione di un documento basato su un oggetto InputStream](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).
1. Aggiungete il contenuto dell&#39;oggetto `com.adobe.idp.Document` all&#39;oggetto `ResourceContent` richiamando il metodo `ResourceContent` dell&#39;oggetto `setDataDocument`. Passa l&#39;oggetto `com.adobe.idp.Document`.
1. Impostare il tipo MIME del file XDP da aggiungere all&#39;archivio richiamando il metodo `ResourceContent` dell&#39;oggetto `setMimeType` e passando `application/vnd.adobe.xdp+xml`.
1. Aggiungete il contenuto dell&#39;oggetto `ResourceContent` all&#39;oggetto `Resource` richiamando il metodo `Resource` object ‘s `setContent` e passando l&#39;oggetto `ResourceContent`.
1. Aggiungete una descrizione della risorsa richiamando l&#39;oggetto `Resource` ‘s `setDescription` e passando un valore di stringa che rappresenta una descrizione della risorsa.
1. Aggiungere la struttura del modulo all&#39;archivio richiamando il metodo `writeResource` dell&#39;oggetto `ResourceRepositoryClient` e passando i valori seguenti:

   * Valore stringa che specifica il percorso della raccolta di risorse contenente la nuova risorsa
   * L&#39;oggetto `Resource` creato

**Consulta anche**

[Avvio rapido (modalità EJB): Creazione di una risorsa tramite l&#39;API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Chiamata  AEM Forms tramite l&#39;API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Richiamo di un processo di breve durata mediante l&#39;API di incitamento {#invoking-a-short-lived-process-using-the-invocation-api}

Potete richiamare un processo di breve durata utilizzando l&#39;API Java Invocation. Quando si richiama un processo di breve durata utilizzando l&#39;API di vocazione, i valori dei parametri richiesti vengono passati utilizzando un oggetto `java.util.HashMap`. Per ogni parametro da passare a un servizio, richiamare il metodo `put` dell&#39;oggetto `java.util.HashMap` e specificare la coppia nome-valore richiesta dal servizio per eseguire l&#39;operazione specificata. Specificate il nome esatto dei parametri che appartengono al processo di breve durata.

>[!NOTE]
>
>Per informazioni su come richiamare un processo di lunga durata, vedere [Richiamo di processi longevi incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

La discussione qui riguarda l&#39;utilizzo di Invocation API per invocare il seguente processo di breve durata  AEM Forms denominato `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms  esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, questo processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Cifra il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

### Richiamare il processo MyApplication/EncryptDocument a breve termine utilizzando l&#39;API di chiamata Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Richiamate il processo di breve durata `MyApplication/EncryptDocument` utilizzando l&#39;API di chiamata Java:

1. Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java. (Vedere [Inclusione  file libreria Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Creare un oggetto `ServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`. Un oggetto `ServiceClient` consente di richiamare un&#39;operazione di servizio. Gestisce attività quali l&#39;individuazione, l&#39;invio e il routing delle richieste di chiamata.
1. Creare un oggetto `java.util.HashMap` utilizzando il relativo costruttore.
1. Richiamare il metodo `java.util.HashMap` dell&#39;oggetto `put` affinché ogni parametro di input passi al processo longevo. Poiché il processo `MyApplication/EncryptDocument` di breve durata richiede un parametro di input di tipo `Document`, è necessario richiamare il metodo `put` solo una volta, come illustrato nell&#39;esempio seguente.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Creare un oggetto `InvocationRequest` richiamando il metodo `ServiceClientFactory` dell&#39;oggetto `createInvocationRequest` e passando i seguenti valori:

   * Un valore di stringa che specifica il nome del processo longevo da richiamare. Per richiamare il processo `MyApplication/EncryptDocument`, specificare `MyApplication/EncryptDocument`.
   * Un valore di stringa che rappresenta il nome dell&#39;operazione di processo. In genere, il nome di un&#39;operazione di processo di breve durata è `invoke`.
   * L&#39;oggetto `java.util.HashMap` che contiene i valori dei parametri richiesti dall&#39;operazione del servizio.
   * Un valore booleano che specifica `true`, che crea una richiesta sincrona (questo valore è applicabile per richiamare un processo di breve durata).

1. Inviare la richiesta di chiamata al servizio richiamando il metodo `invoke` dell&#39;oggetto `InvocationRequest` e passando l&#39;oggetto `ServiceClient`. Il metodo `invoke` restituisce un oggetto `InvocationReponse`.

   >[!NOTE]
   >
   >Un processo di lunga durata può essere invocato trasmettendo il valore `false`come quarto parametro del metodo `createInvocationRequest`. Passando il valore `false`*viene creata una richiesta asincrona.*

1. Recuperare il valore restituito dal processo richiamando il metodo `getOutputParameter` dell&#39;oggetto `InvocationReponse` e passando un valore di stringa che specifica il nome del parametro di output. In questa situazione, specificare `outDoc` ( `outDoc` è il nome del parametro di output per il processo `MyApplication/EncryptDocument`). Inserite il valore restituito in `Document`, come illustrato nell&#39;esempio seguente.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Create un oggetto `java.io.File` e accertatevi che l&#39;estensione del file sia .pdf.
1. Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per copiare nel file il contenuto dell&#39;oggetto `com.adobe.idp.Document`. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` restituito dal metodo `getOutputParameter`.

**Consulta anche**

[Avvio rapido: Richiamo di un processo di breve durata tramite l&#39;API di incitamento](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Richiamo di processi a lunga durata basati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Inclusione  file libreria Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)