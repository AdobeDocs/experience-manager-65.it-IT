---
title: Installazione e configurazione di document services
seo-title: Installing and configuring document services
description: Installa AEM Forms document services per creare, assemblare, distribuire, archiviare documenti PDF, aggiungere firme digitali per limitare l’accesso ai documenti e decodificare Forms con codice a barre.
seo-description: Install AEM Forms document services to create, assemble, distribute, archive PDF documents, add digital signatures to limit access to documents, and decode barcoded forms.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Admin
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
source-git-commit: 2d12f1652a3b8ec4e6ca9c737dc844d1f53f7d08
workflow-type: tm+mt
source-wordcount: '5365'
ht-degree: 2%

---

# Installazione e configurazione di document services {#installing-and-configuring-document-services}

AEM Forms fornisce un set di servizi OSGi per eseguire diverse operazioni a livello di documento, ad esempio servizi per creare, assemblare, distribuire e archiviare documenti PDF, aggiungere firme digitali per limitare l’accesso ai documenti e decodificare Forms con codice a barre. Questi servizi sono inclusi nel pacchetto aggiuntivo di AEM Forms. Collettivamente, questi servizi sono noti come document services. L’elenco dei servizi di documentazione disponibili e le relative funzionalità principali è il seguente:

* **Servizio Assembler:** Consente di combinare, ridisporre e integrare documenti PDF e XDP e di ottenere informazioni sui documenti PDF. Consente inoltre di convertire e convalidare i documenti PDF in PDF/A standard, di trasformare PDF forms, moduli XML e PDF forms in PDF/A-1b, PDF/A-2b e PDFA/A-3b. Per ulteriori informazioni, consulta [Servizio Assembler](/help/forms/using/assembler-service.md).

* **Servizio ConvertPDF:** Consente di convertire i documenti PDF in file PostScript o di immagine (JPEG, JPEG 2000, PNG e TIFF). Per ulteriori informazioni, consulta [Servizio ConvertPDF](/help/forms/using/using-convertpdf-service.md).

* **Servizio Forms barcoded:** Consente di estrarre dati da immagini elettroniche di codici a barre. Il servizio accetta file TIFF e PDF che includono uno o più codici a barre come input ed estrae i dati dei codici a barre. Per ulteriori informazioni, consulta [Servizio Forms barcoded](/help/forms/using/using-barcoded-forms-service.md).

* **Servizio DocAssurance:** Consente di crittografare e decrittografare i documenti, di estendere le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi e di aggiungere firme digitali ai documenti. Il servizio di garanzia documenti contiene tre servizi: firma, crittografia ed estensione del lettore. Per ulteriori informazioni, consulta [Servizio DocAssurance](/help/forms/using/overview-aem-document-services.md).

* **Servizio di crittografia:** Consente di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l&#39;accesso ai relativi contenuti. Per ulteriori informazioni, consulta [Servizio di crittografia](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Servizio Forms:** Consente di creare applicazioni client di acquisizione dati interattive per la convalida, la elaborazione, la trasformazione e la distribuzione di moduli generalmente creati in Forms Designer. Il servizio Forms esegue il rendering di qualsiasi struttura del modulo sviluppata in documenti PDF. Per ulteriori informazioni, consulta [Servizio Forms](/help/forms/using/forms-service.md).

* **Servizio di uscita:** Consente di creare documenti in diversi formati, tra cui PDF, formati di stampante laser e formati di stampa delle etichette. I formati della stampante laser sono PostScript e PCL (Printer Control Language). Per ulteriori informazioni, consulta [Servizio di output](/help/forms/using/output-service.md).

* **Servizio PDF Generator:** Il servizio PDF Generator fornisce API per la conversione dei formati di file nativi in PDF. Converte anche PDF in altri formati di file e ottimizza le dimensioni dei documenti PDF. Per ulteriori informazioni, consulta [Servizio PDF Generator](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Servizio Estensione Reader:** Consente alla tua organizzazione di condividere facilmente i documenti PDF interattivi estendendo le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi. Il servizio attiva le funzioni non disponibili quando un documento di PDF viene aperto tramite Adobe Reader, ad esempio l’aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento. Per ulteriori informazioni, consulta [Servizio di estensione del Reader](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Servizio firma:** Consente di utilizzare firme digitali e documenti sul server AEM. Ad esempio, il servizio Firma viene generalmente utilizzato nelle situazioni seguenti:

   * Il server AEM certifica un modulo prima che venga inviato a un utente per l’apertura utilizzando Acrobat o Adobe Reader.
   * Il server AEM convalida una firma aggiunta a un modulo utilizzando Acrobat o Adobe Reader.
   * Il server AEM firma un modulo per conto di un notaio pubblico.

   Il servizio firma accede ai certificati e alle credenziali archiviati nell’archivio attendibilità. Per ulteriori informazioni, consulta [Servizio Firma](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms è una potente piattaforma di classe enterprise e document services è solo una delle funzionalità di AEM Forms. Per un elenco completo delle funzionalità, consulta [Introduzione ad AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

Il pacchetto aggiuntivo di AEM Forms è un&#39;applicazione distribuita su AEM. In genere, per eseguire AEM Forms Document Services è necessaria una sola istanza AEM (authoring o pubblicazione). Per eseguire AEM Forms document services, si consiglia di utilizzare la seguente topologia. Per informazioni dettagliate sulle topologie, vedi [Architettura e topologie di implementazione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Architettura e topologie di implementazione per AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Sebbene AEM Forms ti consenta di configurare ed eseguire tutte le funzionalità da un singolo server, devi eseguire la pianificazione della capacità, il bilanciamento del carico e configurare server dedicati per funzionalità specifiche in un ambiente di produzione. Ad esempio, per un ambiente che utilizza il servizio PDF Generator per convertire migliaia di pagine al giorno e più moduli adattivi per l’acquisizione dei dati, configura server AEM Forms separati per il servizio PDF Generator e le funzionalità dei moduli adattivi. Consente di fornire prestazioni ottimali e di scalare i server in modo indipendente l&#39;uno dall&#39;altro.

## Requisiti di sistema {#system-requirements}

Prima di iniziare a installare e configurare AEM Forms Document Services, assicurati che:

* L&#39;infrastruttura hardware e software è in funzione. Per un elenco dettagliato dell&#39;hardware e del software supportati, consultare [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell&#39;istanza AEM non contiene spazi bianchi.
* Un&#39;istanza AEM è in esecuzione. Nella terminologia AEM, un&#39;istanza è una copia di AEM in esecuzione su un server in modalità di authoring o pubblicazione. In genere, per eseguire AEM Forms Document Services è necessaria una sola istanza AEM (authoring o pubblicazione):

   * **Autore**: Un’istanza AEM utilizzata per creare, caricare e modificare i contenuti e per amministrare il sito web. Quando il contenuto è pronto per essere live, viene replicato nell’istanza di pubblicazione.
   * **Pubblica**: Un&#39;istanza AEM che trasmette il contenuto pubblicato al pubblico tramite Internet o una rete interna.

* I requisiti di memoria sono soddisfatti. Il pacchetto aggiuntivo di AEM Forms richiede:

   * 15 GB di spazio temporaneo per le installazioni basate su Microsoft® Windows.
   * 6 GB di spazio temporaneo per installazioni basate su UNIX.

* Il software client richiesto per il generatore PDF per eseguire la conversione su Microsoft® Windows e Linux® è installato:

   * **Microsoft® Windows**: Installa [Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) o [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux®**: Installa [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* In Microsoft® Windows, PDF Generator supporta i percorsi di conversione WebKit, Acrobat WebCapture e PhantomJS per convertire i file HTML in documenti PDF.
>* Nei sistemi operativi basati su UNIX, PDF Generator supporta percorsi di conversione WebKit e PhantomJS per convertire i file HTML in documenti PDF.
>


### Requisiti aggiuntivi per il sistema operativo basato su UNIX {#extrarequirements}

Se si utilizza il sistema operativo basato su UNIX, installare i seguenti pacchetti dal supporto di installazione del rispettivo sistema operativo:

<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>espatriare</li>
    </ul> </td>
   <td>
    <ul>
     <li>libxcb</li>
    </ul> </td>
   <td>
    <ul>
     <li>freetype</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXau</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libSM</li>
    </ul> </td>
   <td>
    <ul>
     <li>zlib</li>
    </ul> </td>
   <td>
    <ul>
     <li>libICE</li>
    </ul> </td>
   <td>
    <ul>
     <li>libuuuid</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>glibc</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXext</li>
    </ul> </td>
   <td>
    <ul>
     <li>nss-softokn-freebl</li>
    </ul> </td>
   <td>
    <ul>
     <li>fontconfig</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libX11</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrender</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrandr</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXinerama</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* **(Solo PDF Generator)**) Installa la versione a 32 bit delle librerie libcurl, libcrypto e libssl e crea i seguenti link simbolici. I collegamenti simbolici puntano all&#39;ultima versione delle rispettive librerie:

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(Solo PDF Generator)** Il servizio PDF Generator supporta i percorsi WebKit e PhantomJS per convertire i file HTML in documenti PDF. Per abilitare la conversione per la route PhantomJS, installa le librerie a 64 bit elencate di seguito. In genere, queste librerie sono già installate. Se manca una libreria, installala manualmente:

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

## Configurazioni pre-installazione {#preinstallationconfigurations}

Le configurazioni elencate nella sezione sulle configurazioni di preinstallazione sono applicabili solo al servizio PDF Generator. Se non si configura il servizio PDF Generator, è possibile saltare la sezione relativa alla configurazione di preinstallazione.

### Installare Adobe Acrobat e applicazioni di terze parti {#install-adobe-acrobat-and-third-party-applications}

Se si utilizza il servizio PDF Generator per convertire i formati di file nativi come Microsoft® Word, Microsoft® Excel, Microsoft® PowerPoint, OpenOffice, WordPerfect X7 e Adobe Acrobat in PDF Documents, assicurarsi che queste applicazioni siano installate su AEM Forms Server.

>[!NOTE]
>
>* Se il server AEM Forms si trova in un ambiente offline o protetto e Internet non è disponibile per attivare Adobe Acrobat, consulta [Attivazione offline](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) per istruzioni su come attivare tali istanze di Adobe Acrobat.
>* Adobe Acrobat, Microsoft® Word, Excel e Powerpoint sono disponibili solo per Microsoft® Windows. Se si utilizza il sistema operativo basato su UNIX, installare OpenOffice per convertire i file RTF e i file Microsoft® Office supportati in documenti PDF.
>* Ignora tutte le finestre di dialogo visualizzate dopo l’installazione di Adobe Acrobat e software di terze parti per tutti gli utenti configurati per l’utilizzo del servizio PDF Generator.
>* Avviare il software installato almeno una volta. Ignora tutte le finestre di dialogo per tutti gli utenti configurati per utilizzare il servizio PDF Generator.
>* [Controlla la data di scadenza dei tuoi numeri di serie Adobe Acrobat](https://helpx.adobe.com/enterprise/kb/volume-license-expiration-check.html) e impostare una data per l&#39;aggiornamento della licenza o [trasferire il numero di serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) in base alla data di scadenza.


Dopo aver installato Acrobat, apri Microsoft® Word. Sulla **Acrobat** scheda , fai clic su **Crea PDF** e convertire un file .doc o .docx disponibile sul computer in un documento PDF. Se la conversione ha esito positivo, AEM Forms è pronto per utilizzare Acrobat con il servizio PDF Generator.

### Variabili dell’ambiente di configurazione {#setup-environment-variables}

Imposta le variabili di ambiente per Java Development Kit a 32 bit e 64 bit, applicazioni di terze parti e Adobe Acrobat. Le variabili di ambiente devono contenere il percorso assoluto dell&#39;eseguibile utilizzato per avviare l&#39;applicazione corrispondente. Ad esempio, la tabella seguente elenca le variabili di ambiente per alcune applicazioni:

<table>
 <tbody>
  <tr>
   <td><p><strong>Applicazione</strong></p> </td>
   <td><p><strong>Variabile di ambiente</strong></p> </td>
   <td><p><strong>Esempio</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>JDK (64 bit)</strong></p> </td>
   <td><p>JAVA_HOME</p> </td>
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td>
  </tr>
  <tr>
   <td><p><strong>Adobe Acrobat</strong></p> </td>
   <td><p>Acrobat_PATH</p> </td>
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>Blocco note</strong></p> </td>
   <td><p>Notepad_PATH</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice</strong></p> </td>
   <td><p>OpenOffice_PATH</p> </td>
   <td><p>C:\Program Files (x86)\OpenOffice.org4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Tutte le variabili di ambiente e i rispettivi percorsi sono sensibili all’uso di maiuscole e minuscole.
>* JAVA_HOME, JAVA_HOME_32 e Acrobat_PATH (solo Windows) sono variabili di ambiente obbligatorie.
>* La variabile di ambiente OpenOffice_PATH viene impostata sulla cartella di installazione anziché sul percorso dell&#39;eseguibile.
>* Non impostare variabili di ambiente per applicazioni Microsoft® Office quali Word, PowerPoint, Excel e Project o per AutoCAD. Se queste applicazioni sono installate sul server, il servizio Generate PDF avvia automaticamente queste applicazioni.
>* Sulle piattaforme basate su UNIX, installare OpenOffice come /root. Se OpenOffice non è installato come radice, il servizio PDF Generator non riesce a convertire i documenti OpenOffice in documenti PDF. Se è necessario installare ed eseguire OpenOffice come utente non root, fornire i diritti di sudo all&#39;utente non root.
>* Se si utilizza OpenOffice su una piattaforma basata su UNIX, eseguire il comando seguente per impostare la variabile del percorso:
>
> `export OpenOffice_PATH=/opt/openoffice.org4`

### (Solo per IBM® WebSphere®) Configura il provider di socket SSL IBM® {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Esegui i seguenti passaggi per configurare il provider di socket SSL IBM®:

1. Crea una copia del file java.security. La posizione predefinita del file è `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Apri il file java.security copiato per la modifica.
1. Cambia le fabbriche di socket SSL predefinite per utilizzare le fabbriche JSSE2 invece delle fabbriche IBM® WebSphere® predefinite:

   **Contenuto predefinito:**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **Contenuto modificato:**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. Per abilitare AEM Forms Server all&#39;utilizzo del file java.security aggiornato, all&#39;avvio del server AEM Forms, aggiungi il seguente argomento java:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Solo Windows) Configura l&#39;installazione del servizio di input penna e scrittura a mano {#configure-install-ink-and-handwriting-service}

Se si esegue Microsoft® Windows Server, configurare il servizio Ink e Handwriting. Il servizio è necessario per aprire i file Microsoft® PowerPoint che utilizzano le funzionalità di collegamento di Microsoft® Office:

1. Apri Server Manager. Fai clic sul pulsante **[!UICONTROL Server Manager]** sulla barra di avvio rapido.
1. Fai clic su **[!UICONTROL Aggiungi funzionalità]** in **[!UICONTROL Funzioni]** menu. Seleziona la **[!UICONTROL Servizi di input penna e scrittura a mano]** casella di controllo.
1. **[!UICONTROL Selezionare le funzioni]** finestra di dialogo con **[!UICONTROL Servizi di input penna e scrittura a mano]** selezionato. Fai clic su **[!UICONTROL Installa]** e il servizio è installato.

### (Solo Windows) Configura le impostazioni dei blocchi di file per Microsoft® Office {#configure-the-file-block-settings-for-microsoft-office}

Modificare le impostazioni del centro di attendibilità di Microsoft® Office per consentire al servizio PDF Generator di convertire i file creati con versioni precedenti di Microsoft® Office.

1. Aprire un&#39;applicazione Microsoft® Office. Ad esempio, Microsoft® Word. Passa a **[!UICONTROL File]**> **[!UICONTROL Opzioni]**. Viene visualizzata la finestra di dialogo delle opzioni.

1. Fai clic su **[!UICONTROL Centro protezione]** e fai clic su **[!UICONTROL Impostazioni del Centro protezione]**.
1. In **[!UICONTROL Impostazioni del Centro protezione]**, fai clic su **[!UICONTROL Impostazioni blocco file]**.
1. In **[!UICONTROL Tipo di file]** deseleziona **[!UICONTROL Apri]** per il tipo di file che il servizio PDF Generator deve poter convertire in documenti PDF.

### (Solo Windows) Concedi il privilegio Sostituisci un token a livello di processo {#grant-the-replace-a-process-level-token-privilege}

L&#39;account utente utilizzato per avviare l&#39;application server richiede **Sostituire un token a livello di processo** privilegio. L&#39;account di sistema locale ha **Sostituire un token a livello di processo** per impostazione predefinita. Per i server in esecuzione con un utente del gruppo Amministratori locali, il privilegio deve essere concesso esplicitamente. Esegui i seguenti passaggi per concedere il privilegio:

1. Aprire l&#39;Editor Criteri di gruppo per Microsoft® Windows. Per aprire Editor Criteri di gruppo, fare clic su **[!UICONTROL Inizio]**, tipo **gpedit.msc** nella casella Inizia ricerca e fai clic su **[!UICONTROL Editor Criteri di gruppo]**.
1. Passa a **[!UICONTROL Criteri computer locali]** > **[!UICONTROL Configurazione computer]** > **[!UICONTROL Impostazioni di Windows]** > **[!UICONTROL Impostazioni di protezione]** > **[!UICONTROL Criteri locali]** > **[!UICONTROL Assegnazione diritti utente]** e modifica le **[!UICONTROL Sostituire un token a livello di processo]** e includere il gruppo Administrators.
1. Aggiungi l’utente alla voce Replace a Process Level Token (Sostituisci token a livello di processo).

### (Solo Windows) Abilitare il servizio PDF Generator per i non amministratori {#enable-the-pdf-generator-service-for-non-administrators}

È possibile abilitare un utente non amministratore per l’utilizzo del servizio PDF Generator. Normalmente, solo gli utenti con privilegi amministrativi possono utilizzare il servizio:

1. Crea una variabile di ambiente, PDFG_NON_ADMIN_ENABLED.
1. Imposta il valore della variabile di ambiente su TRUE.
1. Riavvia l&#39;istanza AEM Forms.

### (Solo Windows) Disattiva Controllo account utente (UAC) {#disable-user-account-control-uac}

1. Per accedere all&#39;Utilità di configurazione del sistema, vai a **[!UICONTROL Start > Esegui]** e quindi inserisci **[!UICONTROL MSCONFIG]**.
1. Fai clic sul pulsante **[!UICONTROL Strumenti]** scorri verso il basso e seleziona **[!UICONTROL Modifica impostazioni UAC]**. Fai clic su **[!UICONTROL Launch]** per eseguire il comando in una nuova finestra.
1. Regolare il cursore sul livello di notifica Mai. Al termine, chiudere la finestra del comando e chiudere la finestra Configurazione di sistema.
1. Verifica che l&#39;impostazione del Registro di sistema per UAC sia impostata su 0 (zero). Esegui i seguenti passaggi per verificare:

   1. Microsoft® consiglia di eseguire il backup del registro prima di modificarlo. Per i passaggi dettagliati vedi [Come eseguire il backup e il ripristino del Registro di sistema in Windows](https://support.microsoft.com/en-us/help/322756).
   1. Apri l&#39;editor del Registro di sistema di Microsoft® Windows. Per aprire l&#39;editor del Registro di sistema, vai a Start > Esegui, digita regedit e fai clic su OK.
   1. Accedi a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Assicurarsi che il valore di EnableLUA sia impostato su 0 (zero).
   1. Assicurare il valore di **EnableLUA** è impostato su 0 (zero). Se il valore non è 0, modificare il valore in 0. Chiudi l’editor del Registro di sistema.

1. Riavvia il computer.

### Disattivazione del servizio di segnalazione errori (solo per Windows) {#disable-error-reporting-service}

Durante la conversione di un documento in PDF tramite il servizio PDF Generator su Windows Server, occasionalmente Windows Server segnala che l&#39;eseguibile ha rilevato un problema e deve chiudersi. Tuttavia, non influisce sulla conversione di PDF in quanto continua in background.

Per evitare di ricevere l&#39;errore, è possibile disabilitare la generazione di rapporti sugli errori di Windows. Per ulteriori informazioni sulla disattivazione della generazione di rapporti sugli errori, vedi [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Solo Windows) Configurare la conversione da HTML a PDF {#configure-html-to-pdf-conversion}

Il servizio PDF Generator fornisce percorsi o metodi WebKit, WebCapture e PhantomJS per convertire i file HTML in documenti PDF. In Windows, per abilitare la conversione per i percorsi WebKit e Acrobat WebCapture, copiare il font Unicode nella directory %windir%\fonts.

>[!NOTE]
>
>Ogni volta che installi nuovi font nella cartella dei font, riavvia l’istanza AEM Forms.

### (Solo piattaforme basate su UNIX) Configurazioni supplementari per la conversione da HTML a PDF  {#extra-configurations-for-html-to-pdf-conversion}

Sulle piattaforme basate su UNIX, il servizio PDF Generator supporta i percorsi WebKit e PhantomJS per convertire i file HTML in documenti PDF. Per abilitare la conversione da HTML a PDF, esegui le seguenti configurazioni, applicabili al percorso di conversione preferito:

### (Solo piattaforme basate su UNIX) Attiva il supporto per i font Unicode (solo WebKit) {#enable-support-for-unicode-fonts-webkit-only}

Copiare il font Unicode in una delle seguenti directory in base alle esigenze del sistema:

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris™)

>[!NOTE]
>
>* Su Red Hat® Enterprise Linux® 6.x e versioni successive, i caratteri corriere non sono disponibili. Per installare i font courier, scarica l&#39;archivio font-ibm-type1-1.0.3.zip. Estrai l&#39;archivio in /usr/share/fonts. Crea un collegamento simbolico da /usr/share/X11/fonts a /usr/share/fonts.
>* Elimina tutti i file della cache dei font .lst dalle directory Html2PdfSvc/bin e /usr/share/fonts .
>* Assicurati che le directory /usr/lib/X11/fonts e /usr/share/fonts esistano. Se le directory non esistono, utilizza il comando ln per creare un collegamento simbolico da /usr/share/X11/fonts a /usr/lib/X11/fonts e un altro collegamento simbolico da /usr/share/fonts a /usr/share/X11/fonts. Assicurati anche che i font del corriere siano disponibili in /usr/lib/X11/fonts.
>* Assicurati che tutti i font (Unicode e non-unicode) siano disponibili nella directory /usr/share/fonts o /usr/share/X11/fonts .
>* Quando si esegue il servizio PDF Generator come utente non root, fornire all&#39;utente non root l&#39;accesso in lettura e scrittura a tutte le directory dei font.
>* Ogni volta che installi nuovi font nella cartella dei font, riavvia l’istanza AEM Forms.
>


## Installare il pacchetto aggiuntivo di AEM Forms {#install-aem-forms-add-on-package}

Il pacchetto aggiuntivo di AEM Forms è un&#39;applicazione distribuita su AEM. Il pacchetto contiene AEM Forms Document Services e altre funzionalità di AEM Forms. Esegui i seguenti passaggi per installare il pacchetto:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Tocca **[!UICONTROL Adobe Experience Manager]** che si trova nel menu di intestazione.
1. In **[!UICONTROL Filtri]** sezione:
   1. Seleziona **[!UICONTROL Forms]** dal **[!UICONTROL Soluzione]** elenco a discesa.
   2. Seleziona la versione e digita il pacchetto. È inoltre possibile utilizzare **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Toccare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accettare i termini dell&#39;EULA]**, e tocca **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

   Puoi anche scaricare il pacchetto tramite il collegamento diretto elencato in [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) articolo.

1. Una volta installato il pacchetto, viene richiesto di riavviare l&#39;istanza AEM. **Non arrestare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED smettano di apparire nel `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log e il log è stabile.

## Configurazioni post-installazione {#post-installation-configurations}

### Configurare la delega di avvio per le librerie RSA/BouncyCastle  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Interrompi l&#39;istanza AEM. Passa a [Directory di installazione AEM]\crx-quickstart\conf\ folder. Apri il file sling.properties per la modifica.

   Se utilizzi `[AEM installation directory]\crx-quickstart\bin\start.bat` per avviare un&#39;istanza AEM, modifica le proprietà sling.properties situate in `[AEM_root]\crx-quickstart\`.

1. Aggiungi le seguenti proprietà al file sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (Solo AIX®) Aggiungi le seguenti proprietà al file sling.properties :

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Salva e chiudi il file 

### Configurazione del servizio di gestione dei font  {#configuring-the-font-manager-service}

1. Accedi a [Gestione configurazione AEM](http://localhost:4502/system/console/configMgr) come amministratore.
1. Individua e apri la **[!UICONTROL Manager font CQ-DAM-Handler-Gibson]** servizio. Specifica il percorso delle directory Font di sistema, Font del server di Adobe e Font cliente. Fai clic su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Il tuo diritto di utilizzare i font forniti da soggetti diversi dall&#39;Adobe è disciplinato dai contratti di licenza forniti da tali soggetti con tali font e non è coperto dalla tua licenza per l&#39;uso del software di Adobe. L&#39;Adobe consiglia di rivedere e assicurarsi di essere in conformità con tutti i contratti di licenza applicabili non Adobi prima di utilizzare font non Adobi con il software di Adobe, in particolare per quanto riguarda l&#39;utilizzo di font in un ambiente server.
   > Quando installi nuovi font nella cartella dei font, riavvia l’istanza AEM Forms.

### Configurare un account utente locale per eseguire il servizio PDF Generator  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Per eseguire il servizio PDF Generator è necessario un account utente locale. Per i passaggi necessari per creare un utente locale, vedi [Creare un account utente in Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) oppure creare un account utente nelle piattaforme basate su UNIX.

1. Apri [Configurazione di AEM Forms PDF Generator](http://localhost:4502/libs/fd/pdfg/config/ui.html) pagina.

1. In **[!UICONTROL Account utente]** specificare le credenziali di un account utente locale e fare clic su **[!UICONTROL Invia]**. Se Microsoft® Windows richiede, consentire l&#39;accesso all&#39;utente. Una volta aggiunto con successo, l’utente configurato viene visualizzato sotto il **[!UICONTROL Account utente]** nella sezione **[!UICONTROL Account utente]** scheda .

### Configurare le impostazioni di timeout {#configure-the-time-out-settings}

1. In [Gestione configurazione AEM](http://localhost:4502/system/console/configMgr), individua e apri le **[!UICONTROL Provider ORB Jacorb]** servizio.

   Aggiungi quanto segue al **[!UICONTROL Proprietà personalizzate.name]** campo e fai clic su **[!UICONTROL Salva]**. Imposta il timeout della risposta in sospeso (noto anche come timeout client CORBA) a 600 secondi.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Configura PDF Generator]**. L’URL predefinito è <http://localhost:4502/libs/fd/pdfg/config/ui.html>.

   Apri **[!UICONTROL Configurazione generale]** imposta e modifica il valore dei campi seguenti per l’ambiente:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descrizione</td>
   <td>Valore predefinito</td>
  </tr>
  <tr>
   <td>Timeout conversione server</td>
   <td>Una conversione PDFG rimane attiva per il numero di secondi definiti nel timeout di conversione del server</td>
   <td>270 secondi<br /> </td>
  </tr>
  <tr>
   <td>Scansione di pulizia PDFG in secondi</td>
   <td>Il numero di secondi necessari per eseguire le operazioni post-conversione.<br /> </td>
   <td>3600 secondi</td>
  </tr>
  <tr>
   <td>Scadenza processo in secondi</td>
   <td>Durata per la quale il servizio PDF Generator può eseguire una conversione. Assicurati che il valore dei secondi di scadenza del processo sia maggiore del valore dei secondi di scansione della pulizia PDFG.</td>
   <td>7200 secondi</td>
  </tr>
 </tbody>
</table>

### (Solo Windows) Configura Acrobat per il servizio PDF Generator {#configure-acrobat-for-the-pdf-generator-service}

In Microsoft® Windows, il servizio PDF Generator utilizza Adobe Acrobat per convertire i formati di file supportati in un documento PDF. Esegui i seguenti passaggi per configurare Adobe Acrobat per il servizio PDF Generator:

1. Apri Acrobat e seleziona **[!UICONTROL Modifica]**> **[!UICONTROL Preferenze]**> **[!UICONTROL Updater]**. In Verifica aggiornamenti, deseleziona **[!UICONTROL Installa automaticamente gli aggiornamenti]** e fai clic su **[!UICONTROL OK]**. Chiudi Acrobat.
1. Fare doppio clic su un documento PDF nel sistema. Quando Acrobat viene avviato per la prima volta, vengono visualizzate le finestre di dialogo relative all’accesso, alla schermata di benvenuto e all’EULA. Ignora queste finestre di dialogo per tutti gli utenti configurati per utilizzare PDF Generator.
1. Esegui il file batch dell&#39;utilità PDF Generator per configurare Acrobat per il servizio PDF Generator:

   1. Apri [Gestione pacchetti AEM](http://localhost:4502/crx/packmgr/index.jsp) e scarica il `adobe-aemfd-pdfg-common-pkg-[version].zip` da Gestione pacchetti.
   1. Decomprimi il file .zip scaricato. Apri il prompt dei comandi con privilegi amministrativi.
   1. Passa a [file zip estratto]`\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\adobe-aemfd-pdfg-common-pkg-[version]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]` directory. Esegui il seguente file batch:

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat è configurato per l’esecuzione con il servizio PDF Generator.

1. Esegui [Strumento di preparazione al sistema (SRT)](#SRT) per convalidare l’installazione di Acrobat.

### (Solo Windows) Configura la route principale per la conversione da HTML a PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

Il servizio PDF Generator fornisce più percorsi per convertire i file HTML in documenti PDF: Webkit, Acrobat WebCapture (solo Windows) e PhantomJS. Adobe consiglia di utilizzare la route PhantomJS perché dispone della capacità di gestire il contenuto dinamico e non ha dipendenze da librerie a 32 bit, JDK a 32 bit o non richiede font aggiuntivi. Inoltre, la route PhantomJS non richiede l&#39;accesso a sudo o root per eseguire la conversione.

Il percorso principale predefinito per la conversione da HTML a PDF è Webkit. Per modificare il percorso di conversione:

1. Nell&#39;istanza AEM autore, passa a **[!UICONTROL Strumenti]**> **[!UICONTROL Forms]**> **[!UICONTROL Configura PDF Generator]**.

1. In **[!UICONTROL Configurazione generale]** seleziona il percorso di conversione preferito dalla scheda **[!UICONTROL Percorso principale per le conversioni da HTML a PDF]** a discesa.

### Inizializza archivio attendibilità globale {#intialize-global-trust-store}

Utilizzando la gestione dell&#39;archivio certificati è possibile importare, modificare ed eliminare i certificati ritenuti attendibili nel server per la convalida delle firme digitali e l&#39;autenticazione dei certificati. È possibile importare ed esportare qualsiasi numero di certificati. Dopo l&#39;importazione di un certificato, è possibile modificare le impostazioni di attendibilità e il tipo di archivio attendibilità. Esegui i seguenti passaggi per inizializzare un archivio attendibilità:

1. Accedi all’istanza AEM Forms come amministratore.
1. Vai a  **[!UICONTROL Strumenti]** >  **[!UICONTROL Sicurezza]** >  **[!UICONTROL Archiviazione attendibile]**.
1. Fai clic su  **[!UICONTROL Crea TrustStore]**. Imposta password e tocca **[!UICONTROL Salva]**.

### Impostare i certificati per l&#39;estensione del Reader e il servizio di crittografia {#set-up-certificates-for-reader-extension-and-encryption-service}

Il servizio DocAssurance può applicare diritti di utilizzo ai documenti PDF. Per applicare i diritti di utilizzo ai documenti PDF, configurare i certificati.

Prima di impostare i certificati, assicurati di disporre di un:

* File di certificato (.pfx).

* Password della chiave privata fornita con il certificato.

* Alias chiave privata. Puoi eseguire il comando Java keytool per visualizzare l&#39;alias della chiave privata:
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Password del file del Registro chiavi. Se utilizzi il certificato Estensioni Reader di Adobe, la password del file Registro chiavi è sempre la stessa della password della Chiave privata.

Esegui i seguenti passaggi per configurare i certificati:

1. Accedi all’istanza di AEM Author come amministratore. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
1. Fai clic sul pulsante **[!UICONTROL name]** campo dell’account utente. La **[!UICONTROL Modifica impostazioni utente]** viene visualizzata la pagina . Nell’istanza di AEM Author, i certificati risiedono in un KeyStore. Se non hai creato un KeyStore in precedenza, fai clic su **[!UICONTROL Crea KeyStore]** e impostare una nuova password per KeyStore. Se il server contiene già un KeyStore, salta questo passaggio.  Se utilizzi il certificato Estensioni Reader di Adobe, la password del file Registro chiavi è sempre la stessa della password della Chiave privata.
1. Sulla **[!UICONTROL Modifica impostazioni utente]** , seleziona la **[!UICONTROL KeyStore]** scheda . Espandi la **[!UICONTROL Aggiungi chiave privata dal file dell&#39;archivio chiavi]** e fornisci un alias. L’alias viene utilizzato per eseguire l’operazione Estensioni di Reader.
1. Per caricare il file del certificato, fai clic su **[!UICONTROL Seleziona il file dell&#39;archivio chiavi]** e carica un &lt;filename>file .pfx.

   Aggiungi il **[!UICONTROL Password dell&#39;archivio chiavi]**, **[!UICONTROL Password chiave privata]** e **[!UICONTROL Alias chiave privata]** associato al certificato ai rispettivi campi. Fai clic su **[!UICONTROL Invia]**.

   >[!NOTE]
   >
   >Nell’ambiente di produzione, sostituisci le credenziali di valutazione con le credenziali di produzione. Assicurati di eliminare le credenziali delle estensioni di Reader precedenti prima di aggiornare una credenziale scaduta o di valutazione.

1. Fai clic su **[!UICONTROL Salva e chiudi]** sulla **[!UICONTROL Modifica impostazioni utente]** pagina.

### Abilita AES-256 {#enable-aes}

Per utilizzare la crittografia AES 256 per i file PDF, ottieni e installa i file dei criteri di valutazione della forza illimitata dell’estensione Java Cryptography Extension (JCE). Sostituisci i file local_policy.jar e US_export_policy.jar nella cartella jre/lib/security . Ad esempio, se utilizzi Sun JDK, copia i file scaricati in `[JAVA_HOME]/jre/lib/security` cartella.

Il servizio Assembler dipende dal servizio Estensioni di Reader, servizio Signature, servizio Forms e servizio Output. Esegui i seguenti passaggi per verificare che i servizi richiesti siano operativi:

1. Accedere all’URL `https://'[server]:[port]'/system/console/bundles` come amministratore.
1. Cerca il servizio seguente e assicurati che i servizi siano operativi:

<table>
 <tbody>
  <tr>
   <th>Nome servizio</th>
   <th>Nome bundle</th>
  </tr>
  <tr>
   <td>Servizio Firme</td>
   <td>adobe-aemfd-signatures</td>
  </tr>
  <tr>
   <td>Servizio estensioni Reader</td>
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td>
  </tr>
  <tr>
   <td>Servizio Forms</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td>
  </tr>
  <tr>
   <td>Servizio di output</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td>
  </tr>
 </tbody>
</table>

## Problemi noti e risoluzione dei problemi {#known-issues-and-troubleshooting}

* La conversione da HTML a PDF non riesce se un file di input compresso contiene file HTML con caratteri a doppio byte nei nomi dei file. Per evitare questo problema, non utilizzare caratteri a doppio byte per la denominazione dei file HTML.

* Nei sistemi operativi basati su UNIX, procedi come segue per trovare le librerie mancanti:

1. Accedi a `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Esegui il comando seguente per elencare tutte le librerie richieste da PhantomJS per la conversione da HTML a PDF.

   `ldd phantomjs`

   Esegui il comando seguente per elencare le librerie mancanti.

   `ldd phantomjs | grep not`

1. Installa manualmente le librerie mancanti.

## Strumento di preparazione al sistema (SRT) {#SRT}

Lo strumento Preparazione del sistema controlla se il computer è configurato correttamente per eseguire le conversioni di PDF Generator. Lo strumento genera un rapporto nel percorso specificato. Per eseguire lo strumento:

1. Apri il prompt dei comandi. Passa a `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools` cartella.

1. Esegui il seguente comando dal prompt dei comandi:

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   Il comando genera il rapporto e crea anche il file srt_config.yaml .

   >[!NOTE]
   >
   > * Se il System Readiness Tool segnala che il file pdfgen.api non è disponibile nella cartella dei plug-in di Acrobat, copia il file pdfgen.api dal file `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` nella directory `[Acrobat_root]\Acrobat\plug_ins` directory.
   >
   > * Puoi usare il file srt_config.yaml per configurare diverse impostazioni di . Il formato del file è:


   ```
      # =================================================================
      # SRT Configuration
      # =================================================================
      #Note - follow correct format to avoid parsing failures
      #e.g. <param name>:<space><param value> 
      #locale: (mandatory field)Locale to be used for SRT. Supported locales [en/fr/de/ja].
      locale: en
   
      #aemTempDir: AEM Temp direcotry
      aemTempDir:
   
      #users: provide PDFG converting users list
      #users:
      # - user1
      # - user2
      users:
   
      #profile: select profile to run specific checks. Choose from [LCM], more will be added soon 
      profile:
   
      #outputDir: directory where output files will be saved
      outputDir:
   ```

1. Accedi a `[Path_of_reports_folder]`. Apri il file SystemReadinessTool.html . Verifica il rapporto e risolvi i problemi menzionati.

## Risoluzione dei problemi

Se si verificano problemi anche dopo aver risolto tutti i problemi segnalati dallo strumento SRT, esegui i seguenti controlli:

Prima di eseguire i seguenti controlli, assicurati che [Strumento di preparazione al sistema](#SRT) non segnala alcun errore.

+++ Adobe Acrobat

* Solo [versione supportata](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) di Microsoft® Office (32 bit) e Adobe Acrobat è installato e le finestre di dialogo di apertura vengono annullate.
* Assicurati che Adobe Acrobat Update Service sia disabilitato.
* Assicurati che [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) file batch eseguito con privilegi di amministratore.
* Assicurati che un utente PDF Generator sia aggiunto nell’interfaccia utente di configurazione di PDF.
* Assicurati che [Sostituire un token a livello di processo](#grant-the-replace-a-process-level-token-privilege) viene aggiunta l’autorizzazione per l’utente PDF Generator.
* Verificare che l&#39;aggiunta COM di Acrobat PDFMaker Office sia abilitata per le applicazioni Microsoft Office.

+++

+++Open Office

**Microsoft® Windows**

* Assicurati che [versione supportata](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) di Microsoft Office è installato e le finestre di dialogo di apertura vengono annullate per tutte le applicazioni.
* Assicurati che un utente PDF Generator sia aggiunto nell’interfaccia utente di configurazione di PDF.
* Assicurati che l’utente di PDF Generator sia membro del gruppo di amministratori e del [Sostituire un token a livello di processo](#grant-the-replace-a-process-level-token-privilege) il privilegio è impostato per l&#39;utente.
* Assicurati che l’utente sia configurato nell’interfaccia utente di PDF Generator ed esegua le seguenti azioni:
   1. Accedi a Microsoft® Windows con l’utente PDF Generator.
   1. Aprire le applicazioni Microsoft® Office o Open Office e annullare tutte le finestre di dialogo.
   1. Imposta AdobePDF come stampante predefinita.
   1. Imposta Acrobat come programma predefinito per i file PDF.
   1. Eseguire la conversione manuale utilizzando le opzioni File > Stampa e barra multifunzione Acrobat nelle applicazioni Microsoft Office e annullare tutte le finestre di dialogo.
   1. Terminare tutti i processi relativi alla conversione, come winword.exe, powerpoint.exe ed excel.exe.
   1. Riavvia il server AEM Forms.

**Linux®**

* Assicurati che [versione supportata](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) di Open Office installato, le finestre di dialogo di apertura vengono annullate per tutte le applicazioni e l&#39;avvio delle applicazioni di Office è stato completato.
* Creare una variabile di ambiente `OpenOffice_PATH` e impostarlo per puntare all&#39;installazione di OpenOffice è impostato nel [console](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) o il profilo dt (Device Tree).
* In caso di problemi durante l&#39;installazione di OpenOffice, assicurati che [Librerie a 32 bit](#extrarequirements) necessari per l&#39;installazione di OpenOffice sono disponibili.

+++

Problemi di conversione da +++HTML a PDF

* Assicurati che le directory dei font siano aggiunte nell’interfaccia utente di configurazione di PDF Generator.

**Linux e Solaris (percorso di conversione PhantomJS)**

* Assicurati che la libreria a 32 bit sia disponibile (libicudata.so.42) per la conversione HTMLToPDF basata su Webkit e le librerie a 64 bit (libicudata.so.42 libs sono disponibili per la conversione HTMLoPDF basata su PhantomJS.

* Esegui il seguente comando per elencare le librerie mancanti per phantomjs:

   ```
   ldd phantomjs | grep not
   ```

* Assicurati che la variabile di ambiente JAVA_HOME_32 punti a una posizione corretta.

**Linux® e Solaris™ (percorso di conversione WebKit)**

* Assicurati che le directory `/usr/lib/X11/fonts` e `/usr/share/fonts` esistono. Se le directory non esistono, crea un collegamento simbolico da `/usr/share/X11/fonts` a `/usr/lib/X11/fonts` e un altro collegamento simbolico da `/usr/share/fonts` a `/usr/share/X11/fonts`.

   ```
   ln -s /usr/share/fonts /usr/share/X11/fonts
   
   ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
   ```

* Assicurati che i font di IBM siano copiati in user/share/fonts.
* Assicurati che la vulnerabilità del fantasma fix glibc sia disponibile sul computer. Utilizza il tuo gestore di pacchetti predefinito per aggiornare alla versione più recente di glibc. Include la correzione della vulnerabilità fantasma.
* Assicurati che nel sistema siano installate le versioni più recenti delle librerie curl, libcrypto e libssl a 32 bit. Crea anche collegamenti simbolici `/usr/lib/libcurl.so` (o libcurl.a per AIX®), `/usr/lib/libcrypto.so` (o libcrypto.a per AIX®) e `/usr/lib/libssl.so` (o libssl.a per AIX®) indica le versioni più recenti (a 32 bit) delle rispettive librerie.

* Esegui i seguenti passaggi per il provider di socket SSL IBM®:
   1. Copia il file java.security da `<WAS_Installed_JAVA>\jre\lib\security` in qualsiasi posizione sul server AEM Forms. La posizione predefinita è Posizione predefinita = `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.

   1. Modifica il file java.security nel percorso copiato e modifica le fabbriche di socket SSL predefinite con le fabbriche JSSE2 (utilizza le fabbriche JSSE2 invece di WebSphere®).

      Modifica le seguenti fabbriche socket JSSE predefinite:

      ```
      #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

      con

      ```
      ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

+++

+++ Impossibile aggiungere un utente PDF Generator (PDFG)

* Assicurarsi che Microsoft® Visual C++ 2012 x86 e Microsoft® Visual C++ 2013 x86 (32 bit) ridistribuibili siano installati su Windows.

+++

+++Errori di test di automazione

* Per Microsoft® Office e OpenOffice, eseguire almeno una conversione manualmente (come ogni utente) per garantire che non venga visualizzata alcuna finestra di dialogo durante la conversione. Se viene visualizzata una finestra di dialogo, la ignora. Questa finestra di dialogo non deve essere visualizzata durante la conversione automatica.

* Prima di eseguire l&#39;automazione su un ambiente AEM Forms su OSGi, assicurati che il pacchetto di test sia installato e attivo.

+++

+++Errori di conversione utente multipli

* Verifica i registri del server per verificare se la conversione non riesce per un particolare utente.(Process Explorer può essere utile per controllare il processo in esecuzione per utenti diversi)

* Assicurati che l’utente configurato per PDF Generator disponga dei diritti di amministrazione locali.

* Assicurati che l’utente PDF Generator abbia le autorizzazioni di lettura, scrittura ed esecuzione sugli utenti temporanei LC e PDFG.

* Per Microsoft® Office e OpenOffice, eseguire almeno una conversione manualmente (come ogni utente) per garantire che non venga visualizzata alcuna finestra di dialogo durante la conversione. Se viene visualizzata una finestra di dialogo, la ignora. Questa finestra di dialogo non deve essere visualizzata durante la conversione automatica.

* Esegui una conversione di esempio.

+++

Scadenza ++ licenza di Adobe Acrobat installato su AEM Forms Server

* Se disponi di una licenza esistente di Adobe Acrobat ed è scaduta, [Scarica la versione più recente di Adobe Application Manager](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html)e la migrazione del numero di serie. Prima [migrazione del numero di serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * Utilizza i seguenti comandi per generare prov.xml e serializzare nuovamente l&#39;installazione esistente utilizzando il file prov.xml invece dei comandi forniti in [migrazione del numero di serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) numero articolo.

          &quot;
          
          adobe_prtk —tool=VolumeSerialize —generate —serial=&lt;serialnum> [—leid=&lt;leid>] [—regsuppress=ss] [—eulasuppress] [—locales=elenco limitato di impostazioni internazionali in formato xx_XX o ALL>] [—provfile=&lt;absolute path=&quot;&quot; to=&quot;&quot; prov.xml=&quot;&quot;>]
          
          &quot;
      
   * Il volume serializza il pacchetto (ri-serializza l&#39;installazione esistente utilizzando il file prov.xml e la nuova serie): Esegui il seguente comando dalla cartella di installazione PRTK come amministratore per serializzare e attivare i pacchetti distribuiti sui computer client:

          &quot;
          adobe_prtk —tool=VolumeSerialize —provfile=C:\prov.xml -stream
          
          &quot;
      
* Per installazioni su larga scala, utilizzare il [Customization Wizard Acrobat](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) per rimuovere le versioni precedenti di Reader e Acrobat. Personalizza il programma di installazione e distribuiscilo a tutti i computer della tua organizzazione.

+++

+++ AEM Forms Server si trova in un ambiente offline o protetto e Internet non è disponibile per attivare Acrobat.

* È possibile accedere online entro 7 giorni dal primo avvio del prodotto di Adobe per completare l&#39;attivazione e la registrazione online oppure utilizzare un dispositivo abilitato per Internet e il numero di serie del prodotto per completare il processo. Per istruzioni dettagliate, vedi [Attivazione offline](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++

## Passaggi successivi {#next-steps}

È disponibile un ambiente AEM Forms Document Services funzionante. È possibile utilizzare document services tramite:

* [Flussi di lavoro incentrati sui moduli su OSGi](/help/forms/using/aem-forms-workflow.md)
* [Cartelle controllate](/help/forms/using/watched-folder-in-aem-forms.md)
* [API di Document Services](/help/forms/using/aem-document-services-programmatically.md)
