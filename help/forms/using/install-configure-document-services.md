---
title: Installazione e configurazione di document services
seo-title: Installazione e configurazione di document services
description: Installare AEM Forms Document Services per creare, assemblare, distribuire, archiviare documenti PDF, aggiungere firme digitali per limitare l’accesso ai documenti e decodificare moduli con codice a barre.
seo-description: Installare AEM Forms Document Services per creare, assemblare, distribuire, archiviare documenti PDF, aggiungere firme digitali per limitare l’accesso ai documenti e decodificare moduli con codice a barre.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Admin
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '4295'
ht-degree: 2%

---

# Installazione e configurazione di document services {#installing-and-configuring-document-services}

AEM Forms fornisce un set di servizi OSGi per eseguire diverse operazioni a livello di documento, ad esempio servizi per creare, assemblare, distribuire e archiviare documenti PDF, aggiungere firme digitali per limitare l’accesso ai documenti e decodificare moduli con codice a barre. Questi servizi sono inclusi nel pacchetto aggiuntivo di AEM Forms. Collettivamente, questi servizi sono noti come document services. L’elenco dei servizi di documentazione disponibili e le relative funzionalità principali è il seguente:

* **Servizio Assembler:** consente di combinare, ridisporre e integrare documenti PDF e XDP e di ottenere informazioni sui documenti PDF. Consente inoltre di convertire e convalidare i documenti PDF in PDF/A standard, di trasformare PDF forms, moduli XML e PDF forms in PDF/A-1b, PDF/A-2b e PDFA/A-3b. Per ulteriori informazioni, vedere [Servizio Assembler](/help/forms/using/assembler-service.md).

* **Servizio ConvertPDF:** consente di convertire i documenti PDF in file PostScript o di immagine (JPEG, JPEG 2000, PNG e TIFF). Per ulteriori informazioni, vedere [ConvertPDF Service](/help/forms/using/using-convertpdf-service.md).

* **Servizio Forms con codice a barre:** consente di estrarre dati da immagini elettroniche di codici a barre. Il servizio accetta file TIFF e PDF che includono uno o più codici a barre come input ed estrae i dati dei codici a barre. Per ulteriori informazioni, consulta [Servizio Forms con codice a barre](/help/forms/using/using-barcoded-forms-service.md).

* **Servizio DocAssurance:** consente di crittografare e decrittografare i documenti, estendere le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi e aggiungere firme digitali ai documenti. Il servizio di garanzia documenti contiene tre servizi: firma, crittografia ed estensione del lettore. Per ulteriori informazioni, vedere [Servizio DocAssurance](/help/forms/using/overview-aem-document-services.md).

* **Servizio di crittografia:** consente di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l&#39;accesso ai relativi contenuti. Per ulteriori informazioni, consulta [Servizio di crittografia](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Servizio Forms:** consente di creare applicazioni client di acquisizione dati interattive per la convalida, la elaborazione, la trasformazione e la distribuzione di moduli generalmente creati in Forms Designer. Il servizio Forms esegue il rendering di tutte le strutture del modulo sviluppate in documenti PDF. Per ulteriori informazioni, consulta [Servizio Forms](/help/forms/using/forms-service.md).

* **Servizio di output:** consente di creare documenti in diversi formati, inclusi PDF, formati stampante laser e formati stampante per etichette. I formati della stampante laser sono PostScript e PCL (Printer Control Language). Per ulteriori informazioni, consulta [Servizio di output](/help/forms/using/output-service.md).

* **Servizio PDF Generator:** il servizio PDF Generator fornisce API per convertire i formati di file nativi in PDF. Converte anche i PDF in altri formati di file e ottimizza le dimensioni dei documenti PDF. Per ulteriori informazioni, vedere [Servizio PDF Generator](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Servizio di estensione del Reader:** consente alla tua organizzazione di condividere facilmente i documenti PDF interattivi estendendo le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi. Il servizio attiva le funzioni non disponibili all’apertura di un documento PDF tramite Adobe Reader, ad esempio l’aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento. Per ulteriori informazioni, consulta [Servizio di estensione del Reader](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Servizio firma:** consente di utilizzare firme digitali e documenti sul server AEM. Ad esempio, il servizio Firma viene generalmente utilizzato nelle situazioni seguenti:

   * Il server AEM certifica un modulo prima che venga inviato a un utente per l’apertura utilizzando Acrobat o Adobe Reader.
   * Il server AEM convalida una firma aggiunta a un modulo utilizzando Acrobat o Adobe Reader.
   * Il server AEM firma un modulo per conto di un notaio pubblico.

   Il servizio firma accede ai certificati e alle credenziali archiviati nell’archivio attendibilità. Per ulteriori informazioni, vedere [Servizio firma](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms è una potente piattaforma di classe enterprise e document services è solo una delle funzionalità di AEM Forms. Per l&#39;elenco completo delle funzionalità, consulta [Introduzione ad AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

Il pacchetto aggiuntivo di AEM Forms è un&#39;applicazione distribuita su AEM. In genere, per eseguire AEM Forms Document Services è necessaria una sola istanza AEM (authoring o pubblicazione). Per eseguire AEM Forms document services, si consiglia di utilizzare la seguente topologia. Per informazioni dettagliate sulle topologie, vedere [Architettura e topologie di distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Architettura e topologie di implementazione per AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Sebbene AEM Forms ti consenta di configurare ed eseguire tutte le funzionalità da un singolo server, devi eseguire la pianificazione della capacità, il bilanciamento del carico e configurare server dedicati per funzionalità specifiche in un ambiente di produzione. Ad esempio, per un ambiente che utilizza il servizio PDF Generator per convertire migliaia di pagine al giorno e più moduli adattivi per l’acquisizione dei dati, impostare server AEM Forms separati per il servizio PDF Generator e le funzionalità dei moduli adattivi. Consente di fornire prestazioni ottimali e di scalare i server in modo indipendente l&#39;uno dall&#39;altro.

## Requisiti di sistema {#system-requirements}

Prima di iniziare a installare e configurare AEM Forms Document Services, assicurati che:

* L&#39;infrastruttura hardware e software è in funzione. Per un elenco dettagliato dell&#39;hardware e del software supportati, vedere [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell&#39;istanza AEM non contiene spazi bianchi.
* Un&#39;istanza AEM è in esecuzione. Nella terminologia AEM, un&#39;istanza è una copia di AEM in esecuzione su un server in modalità di authoring o pubblicazione. In genere, per eseguire AEM Forms Document Services è necessaria una sola istanza AEM (authoring o pubblicazione):

   * **Autore**: Un’istanza AEM utilizzata per creare, caricare e modificare i contenuti e per amministrare il sito web. Quando il contenuto è pronto per essere live, viene replicato nell’istanza di pubblicazione.
   * **Pubblica**: Un&#39;istanza AEM che trasmette il contenuto pubblicato al pubblico tramite Internet o una rete interna.

* I requisiti di memoria sono soddisfatti. Il pacchetto aggiuntivo di AEM Forms richiede:

   * 15 GB di spazio temporaneo per le installazioni basate su Microsoft Windows.
   * 6 GB di spazio temporaneo per installazioni basate su UNIX.

* Il software client necessario per il generatore PDF per eseguire la conversione su Microsoft Windows e Linux è installato:

   * **Microsoft Windows**: Installa  [Microsoft ](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)Office o  [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux**: Installa  [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* In Microsoft Windows, PDF Generator supporta i percorsi di conversione WebKit, Acrobat WebCapture e PhantomJS per convertire i file HTML in documenti PDF.
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

* **(Solo** PDF Generator) Installa la versione a 32 bit delle librerie libcurl, libcrypto e libssl e crea i seguenti link simbolici. I collegamenti simbolici puntano all&#39;ultima versione delle rispettive librerie:

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

Se si utilizza il servizio PDF Generator per convertire i formati di file nativi come Microsoft Word, Microsoft Excel, Microsoft PowerPoint, OpenOffice, WordPerfect X7 e Adobe Acrobat in documenti PDF, verificare che tali applicazioni siano installate sul server AEM Forms.

>[!NOTE]
>
>* Adobe Acrobat, Microsoft Word, Excel e Powerpoint sono disponibili solo per Microsoft Windows. Se si utilizza il sistema operativo basato su UNIX, installare OpenOffice per convertire i file RTF e i file supportati di Microsoft Office in documenti PDF.
>* Ignora tutte le finestre di dialogo visualizzate dopo l’installazione di Adobe Acrobat e software di terze parti per tutti gli utenti configurati per l’utilizzo del servizio PDF Generator.
>* Avviare il software installato almeno una volta. Ignora tutte le finestre di dialogo per tutti gli utenti configurati per utilizzare il servizio PDF Generator.

>



Dopo aver installato Acrobat, apri Microsoft Word. Nella scheda **Acrobat** fare clic su **Crea PDF** e convertire un file .doc o .docx disponibile sul computer in un documento PDF. Se la conversione ha esito positivo, AEM Forms è pronto per utilizzare Acrobat con il servizio PDF Generator.

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
   <td><p><strong>JDK (32 bit)</strong></p> </td> 
   <td><p>JAVA_HOME_32</p> </td> 
   <td><p>C:\Program Files (x86)\Java\jdk1.8.0_74</p> </td> 
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
>* Non impostare variabili di ambiente per applicazioni di Microsoft Office quali Word, PowerPoint, Excel e Project o per AutoCAD. Se queste applicazioni sono installate sul server, il servizio Genera PDF avvia automaticamente queste applicazioni.
>* Sulle piattaforme basate su UNIX, installare OpenOffice come /root. Se OpenOffice non è installato come radice, il servizio PDF Generator non riesce a convertire i documenti OpenOffice in documenti PDF. Se è necessario installare ed eseguire OpenOffice come utente non root, fornire i diritti di sudo all&#39;utente non root.
>* Se si utilizza OpenOffice su una piattaforma basata su UNIX, eseguire il comando seguente per impostare la variabile del percorso:

>
>  
`export OpenOffice_PATH=/opt/openoffice.org4`

### (Solo per IBM WebSphere) Configura provider di socket SSL IBM {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Esegui i seguenti passaggi per configurare il provider di socket SSL IBM:

1. Crea una copia del file java.security. Il percorso predefinito del file è `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Apri il file java.security copiato per la modifica.
1. Cambia le fabbriche di socket SSL predefinite per utilizzare le fabbriche JSSE2 invece delle fabbriche IBM WebSphere predefinite:

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

1. Per consentire al server AEM Forms di utilizzare il file java.security aggiornato, all&#39;avvio del server AEM Forms, aggiungi il seguente argomento java:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Solo Windows) Configura l&#39;installazione del servizio di input penna e scrittura a mano {#configure-install-ink-and-handwriting-service}

Se si esegue Microsoft Windows Server, configurare il servizio Ink e Handwriting. Il servizio è necessario per aprire i file Microsoft PowerPoint che utilizzano le funzionalità di collegamento di Microsoft Office:

1. Apri Server Manager. Fare clic sull&#39;icona **[!UICONTROL Server Manager]** nella barra di avvio rapido.
1. Fare clic su **[!UICONTROL Aggiungi funzionalità]** nel menu **[!UICONTROL Caratteristiche]**. Selezionare la casella di controllo **[!UICONTROL Servizi di input penna e scrittura a mano]**.
1. **[!UICONTROL Selezionare]** la finestra di dialogo Caratteristiche con  **[!UICONTROL Inchiostro e]** Servizi di scrittura a mano selezionata. Fai clic su **[!UICONTROL Installa]** per installare il servizio.

### (Solo Windows) Configurare le impostazioni dei blocchi di file per Microsoft Office {#configure-the-file-block-settings-for-microsoft-office}

Modificare le impostazioni del centro di protezione di Microsoft Office per consentire al servizio PDF Generator di convertire i file creati con versioni precedenti di Microsoft Office.

1. Aprire un&#39;applicazione di Microsoft Office. Ad esempio, Microsoft Word. Passa a **[!UICONTROL File]**> **[!UICONTROL Opzioni]**. Viene visualizzata la finestra di dialogo delle opzioni.

1. Fare clic su **[!UICONTROL Centro protezione]**, quindi fare clic su **[!UICONTROL Impostazioni centro protezione]**.
1. In **[!UICONTROL Impostazioni Centro protezione]**, fare clic su **[!UICONTROL Impostazioni blocco file]**.
1. Nell&#39;elenco **[!UICONTROL Tipo di file]**, deselezionare **[!UICONTROL Apri]** per il tipo di file che il servizio PDF Generator deve poter convertire in documenti PDF.

### (Solo Windows) Concedi il privilegio Sostituisci un token a livello di processo {#grant-the-replace-a-process-level-token-privilege}

L&#39;account utente utilizzato per avviare l&#39;application server richiede il privilegio **Replace a process level token** . Per impostazione predefinita, l&#39;account di sistema locale dispone del privilegio **Replace a process level token** . Per i server in esecuzione con un utente del gruppo Amministratori locali, il privilegio deve essere concesso esplicitamente. Esegui i seguenti passaggi per concedere il privilegio:

1. Aprire l&#39;Editor Criteri di gruppo per Microsoft Windows. Per aprire l&#39;Editor Criteri di gruppo, fare clic su **[!UICONTROL Start]**, digitare **gpedit.msc** nella casella Cerca iniziale e fare clic su **[!UICONTROL Editor Criteri di gruppo]**.
1. Passa a **[!UICONTROL Criteri computer locali]** > **[!UICONTROL Configurazione computer]** > **[!UICONTROL Impostazioni di Windows]** > **[!UICONTROL Impostazioni di sicurezza]** > **[!UICONTROL Criteri locali]** > **[!UICONTROL Assegnazione diritti utente]** e modifica il **[!UICONTROL Sostituisci a token a livello di processo]** e include il gruppo Administrators.
1. Aggiungi l’utente alla voce Replace a Process Level Token (Sostituisci token a livello di processo).

### (Solo Windows) Abilita il servizio PDF Generator per i non amministratori {#enable-the-pdf-generator-service-for-non-administrators}

È possibile abilitare un utente non amministratore all&#39;utilizzo del servizio PDF Generator. Normalmente, solo gli utenti con privilegi amministrativi possono utilizzare il servizio:

1. Crea una variabile di ambiente, PDFG_NON_ADMIN_ENABLED.
1. Imposta il valore della variabile di ambiente su TRUE.
1. Riavvia l&#39;istanza AEM Forms.

### (Solo Windows) Disattiva Controllo account utente (UAC) {#disable-user-account-control-uac}

1. Per accedere all&#39;Utilità di configurazione del sistema, vai a **[!UICONTROL Start > Esegui]**, quindi immetti **[!UICONTROL MSCONFIG]**.
1. Fai clic sulla scheda **[!UICONTROL Strumenti]** , scorri verso il basso e seleziona **[!UICONTROL Cambia impostazioni UAC]**. Fai clic su **[!UICONTROL Launch]** per eseguire il comando in una nuova finestra.
1. Regolare il cursore sul livello di notifica Mai. Al termine, chiudere la finestra del comando e chiudere la finestra Configurazione di sistema.
1. Verifica che l&#39;impostazione del Registro di sistema per UAC sia impostata su 0 (zero). Esegui i seguenti passaggi per verificare:

   1. Microsoft consiglia di eseguire il backup del Registro di sistema prima di modificarlo. Per passaggi dettagliati, vedere [Come eseguire il backup e il ripristino del Registro di sistema in Windows](https://support.microsoft.com/en-us/help/322756).
   1. Apri l&#39;editor del Registro di sistema di Microsoft Windows. Per aprire l&#39;editor del Registro di sistema, vai a Start > Esegui, digita regedit e fai clic su OK.
   1. Accedi a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Assicurarsi che il valore di EnableLUA sia impostato su 0 (zero).
   1. Assicurati che il valore di **EnableLUA** sia impostato su 0 (zero). Se il valore non è 0, modificare il valore in 0. Chiudi l’editor del Registro di sistema.

1. Riavvia il computer.

### Disattivazione del servizio di segnalazione errori (solo per Windows) {#disable-error-reporting-service}

Durante la conversione di un documento in PDF utilizzando il servizio PDF Generator su Windows Server, occasionalmente Windows Server segnala che l&#39;eseguibile ha rilevato un problema e deve essere chiuso. Tuttavia, non influisce sulla conversione PDF in quanto continua in background.

Per evitare di ricevere l&#39;errore, è possibile disabilitare la generazione di rapporti sugli errori di Windows. Per ulteriori informazioni sulla disattivazione della generazione di rapporti sugli errori, consulta [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Solo Windows) Configura la conversione da HTML a PDF {#configure-html-to-pdf-conversion}

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
* /usr/openwin/lib/X11/fonts/TrueType (Solaris)

>[!NOTE]
>
>* Su RedHat Enterprise Linux 6.x e versioni successive, i caratteri corriere non sono disponibili. Per installare i font courier, scarica l&#39;archivio font-ibm-type1-1.0.3.zip. Estrai l&#39;archivio in /usr/share/fonts. Crea un collegamento simbolico da /usr/share/X11/fonts a /usr/share/fonts.
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
1. Nella sezione **[!UICONTROL Filtri]** :
   1. Seleziona **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Seleziona la versione e digita il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Tocca il nome del pacchetto applicabile al tuo sistema operativo, seleziona **[!UICONTROL Accetta termini EULA]** e tocca **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://docs.adobe.com/content/help/it/experience-manager-65/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

   Puoi anche scaricare il pacchetto tramite il collegamento diretto elencato nell&#39;articolo [Versioni di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) .

1. Una volta installato il pacchetto, viene richiesto di riavviare l&#39;istanza AEM. **Non arrestare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED smettano di apparire nel file  `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log e il registro sia stabile.

## Configurazioni post-installazione {#post-installation-configurations}

### Configurare la delega di avvio per le librerie RSA/BouncyCastle  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Interrompi l&#39;istanza AEM. Passa alla [directory di installazione AEM]\crx-quickstart\conf\ folder. Apri il file sling.properties per la modifica.

   Se utilizzi `[AEM installation directory]\crx-quickstart\bin\start.bat` per avviare un&#39;istanza AEM, modifica le proprietà sling.properties che si trovano in `[AEM_root]\crx-quickstart\`.

1. Aggiungi le seguenti proprietà al file sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (Solo AIX) Aggiungi le seguenti proprietà al file sling.properties :

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Salva e chiudi il file 

### Configurazione del servizio di gestione dei font  {#configuring-the-font-manager-service}

1. Accedi a [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) come amministratore.
1. Individua e apri il servizio **[!UICONTROL CQ-DAM-Handler-Gibson Font Managers]** . Specifica il percorso delle directory Font di sistema, Font del server di Adobe e Font cliente. Fai clic su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Il tuo diritto di utilizzare i font forniti da soggetti diversi dall&#39;Adobe è disciplinato dai contratti di licenza forniti da tali soggetti con tali font e non è coperto dalla tua licenza per l&#39;uso del software di Adobe. L&#39;Adobe consiglia di rivedere e assicurarsi di essere in conformità con tutti i contratti di licenza applicabili non Adobi prima di utilizzare font non Adobi con il software di Adobe, in particolare per quanto riguarda l&#39;utilizzo di font in un ambiente server.
   > Quando installi nuovi font nella cartella dei font, riavvia l’istanza AEM Forms.

### Configurare un account utente locale per eseguire il servizio PDF Generator  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Per eseguire il servizio PDF Generator è necessario un account utente locale. Per i passaggi necessari per creare un utente locale, vedere [Creare un account utente in Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) o [creare un account utente nelle piattaforme basate su UNIX](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html).

1. Apri la pagina [AEM Forms PDF Generator Configuration](http://localhost:4502/libs/fd/pdfg/config/ui.html) .

1. Nella scheda **[!UICONTROL Account utente]**, specificare le credenziali di un account utente locale e fare clic su **[!UICONTROL Invia]**. Se viene richiesto da Microsoft Windows, consentire l&#39;accesso all&#39;utente. Una volta aggiunto correttamente, l&#39;utente configurato viene visualizzato nella sezione **[!UICONTROL Account utente]** della scheda **[!UICONTROL Account utente]** .

### Configurare le impostazioni di timeout {#configure-the-time-out-settings}

1. In [AEM configuration manager](http://localhost:4502/system/console/configMgr), individua e apri il servizio **[!UICONTROL Provider ORB Jacorb]** .

   Aggiungi quanto segue al campo **[!UICONTROL Proprietà personalizzate]** e fai clic su **[!UICONTROL Salva]**. Imposta il timeout della risposta in sospeso (noto anche come timeout client CORBA) a 600 secondi.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Configura PDF Generator]**. L’URL predefinito è http://localhost:4502/libs/fd/pdfg/config/ui.html.

   Apri la scheda **[!UICONTROL Configurazione generale]** e modifica il valore dei campi seguenti per il tuo ambiente:

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

In Microsoft Windows, il servizio PDF Generator utilizza Adobe Acrobat per convertire i formati di file supportati in un documento PDF. Esegui i seguenti passaggi per configurare Adobe Acrobat per il servizio PDF Generator:

1. Apri Acrobat e seleziona **[!UICONTROL Modifica]**> **[!UICONTROL Preferenze]**> **[!UICONTROL Updater]**. In Verifica aggiornamenti, deselezionare **[!UICONTROL Installa automaticamente gli aggiornamenti]** e fare clic su **[!UICONTROL OK]**. Chiudi Acrobat.
1. Fare doppio clic su un documento PDF nel sistema. Quando Acrobat viene avviato per la prima volta, vengono visualizzate le finestre di dialogo relative all’accesso, alla schermata di benvenuto e all’EULA. Ignora queste finestre di dialogo per tutti gli utenti configurati per utilizzare PDF Generator.
1. Esegui il file batch dell&#39;utilità PDF Generator per configurare Acrobat per il servizio PDF Generator:

   1. Apri [AEM Package Manager](http://localhost:4502/crx/packmgr/index.jsp) e scarica il file `adobe-aemfd-pdfg-common-pkg-[version].zip` dal package manager.
   1. Decomprimi il file .zip scaricato. Apri il prompt dei comandi con privilegi amministrativi.
   1. Passa alla directory `[extracted-zip-file]\jcr_root\etc\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\scripts` . Esegui il seguente file batch:

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat è configurato per l’esecuzione con il servizio PDF Generator.

1. Esegui System Readiness Tool (SRT) per convalidare l’installazione di Acrobat. Lo strumento controlla se il computer è configurato correttamente per eseguire le conversioni di PDF Generator e genera un rapporto nel percorso specificato:

   1. Apri il prompt dei comandi. Passa alla cartella `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\etc\fd\ pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\srt` . Esegui il seguente comando dal prompt dei comandi:

      `cscript SystemReadinessTool.vbs [Path_of_reports_folder] en`

      >[!NOTE]
      >
      >Se il System Readiness Tool segnala che il file pdfgen.api non è disponibile nella cartella dei plug-in di acrobat, copia il file pdfgen.api dalla directory `[extracted-adobe-aemfd-pdfg-common-pkg]\plugins\x86_win32` alla directory `[Acrobat_root]\Acrobat\plug_ins`.

   1. Accedi a `[Path_of_reports_folder]`. Apri il file SystemReadinessTool.html . Verifica il rapporto e risolvi i problemi menzionati.

### (Solo Windows) Configura il percorso principale per la conversione da HTML a PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

Il servizio PDF Generator fornisce più percorsi per convertire i file HTML in documenti PDF: Webkit, Acrobat WebCapture (solo Windows) e PhantomJS. Adobe consiglia di utilizzare la route PhantomJS perché dispone della capacità di gestire il contenuto dinamico e non ha dipendenze da librerie a 32 bit, JDK a 32 bit o non richiede font aggiuntivi. Inoltre, la route PhantomJS non richiede l&#39;accesso a sudo o root per eseguire la conversione.

La via principale predefinita per la conversione da HTML a PDF è Webkit. Per modificare il percorso di conversione:

1. Nell&#39;istanza AEM autore, passa a **[!UICONTROL Strumenti]**> **[!UICONTROL Forms]**> **[!UICONTROL Configura PDF Generator]**.

1. Nella scheda **[!UICONTROL Configurazione generale]** , seleziona il percorso di conversione preferito dal menu a discesa **[!UICONTROL Route principale per conversioni da HTML a PDF]** .

### Inizializza archivio attendibilità globale {#intialize-global-trust-store}

Utilizzando la gestione dell&#39;archivio certificati è possibile importare, modificare ed eliminare i certificati ritenuti attendibili nel server per la convalida delle firme digitali e l&#39;autenticazione dei certificati. È possibile importare ed esportare qualsiasi numero di certificati. Dopo l&#39;importazione di un certificato, è possibile modificare le impostazioni di attendibilità e il tipo di archivio attendibilità. Esegui i seguenti passaggi per inizializzare un archivio attendibilità:

1. Accedi all’istanza AEM Forms come amministratore.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Archivio fonti attendibili]**.
1. Fare clic su **[!UICONTROL Crea TrustStore]**. Imposta la password e tocca **[!UICONTROL Salva]**.

### Impostare i certificati per l&#39;estensione del Reader e il servizio di crittografia {#set-up-certificates-for-reader-extension-and-encryption-service}

Il servizio DocAssurance può applicare diritti di utilizzo ai documenti PDF. Per applicare diritti di utilizzo ai documenti PDF, configurare i certificati.

Prima di impostare i certificati, assicurati di disporre di un:

* File di certificato (.pfx).

* Password della chiave privata fornita con il certificato.

* Alias chiave privata. Puoi eseguire il comando Java keytool per visualizzare l&#39;alias della chiave privata:
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Password del file del Registro chiavi. Se utilizzi il certificato Estensioni Reader di Adobe, la password del file Registro chiavi è sempre la stessa della password della Chiave privata.

Esegui i seguenti passaggi per configurare i certificati:

1. Accedi all’istanza di AEM Author come amministratore. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
1. Fare clic sul campo **[!UICONTROL name]** dell&#39;account utente. Viene visualizzata la pagina **[!UICONTROL Modifica impostazioni utente]**. Nell’istanza di AEM Author, i certificati risiedono in un KeyStore. Se non hai creato un KeyStore in precedenza, fai clic su **[!UICONTROL Crea KeyStore]** e imposta una nuova password per KeyStore. Se il server contiene già un KeyStore, salta questo passaggio.  Se utilizzi il certificato Estensioni Reader di Adobe, la password del file Registro chiavi è sempre la stessa della password della Chiave privata.
1. Nella pagina **[!UICONTROL Modifica impostazioni utente]**, seleziona la scheda **[!UICONTROL KeyStore]** . Espandi l’opzione **[!UICONTROL Aggiungi chiave privata dal file dell’archivio chiavi]** e fornisci un alias. L’alias viene utilizzato per eseguire l’operazione Estensioni di Reader.
1. Per caricare il file del certificato, fai clic su **[!UICONTROL Seleziona File archivio chiavi]** e carica un file &lt;filename>.pfx.

   Aggiungi i **[!UICONTROL Password archivio chiavi]**, **[!UICONTROL Password chiave privata]** e **[!UICONTROL Alias chiave privata]** associati al certificato ai rispettivi campi. Fare clic su **[!UICONTROL Invia]**.

   >[!NOTE]
   >
   >Nell’ambiente di produzione, sostituisci le credenziali di valutazione con le credenziali di produzione. Assicurati di eliminare le credenziali delle estensioni di Reader precedenti prima di aggiornare una credenziale scaduta o di valutazione.

1. Fare clic su **[!UICONTROL Salva e chiudi]** nella pagina **[!UICONTROL Modifica impostazioni utente]**.

### Abilita AES-256 {#enable-aes}

Per utilizzare la crittografia AES 256 per i file PDF, ottieni e installa i file dei criteri di valutazione della forza illimitata dell’estensione Java Cryptography Extension (JCE). Sostituisci i file local_policy.jar e US_export_policy.jar nella cartella jre/lib/security . Ad esempio, se utilizzi Sun JDK, copia i file scaricati nella cartella `[JAVA_HOME]/jre/lib/security` .

Il servizio Assembler dipende dal servizio Estensioni di Reader, servizio Signature, servizio Forms e servizio Output. Esegui i seguenti passaggi per verificare che i servizi richiesti siano operativi:

1. Accedi all&#39;URL `https://'[server]:[port]'/system/console/bundles` come amministratore.
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

1. Esegui il comando seguente per elencare tutte le librerie necessarie per la conversione da HTML a PDF da PhantomJS.

   `ldd phantomjs`

   Esegui il comando seguente per elencare le librerie mancanti.

   `ldd phantomjs | grep not`

1. Installa manualmente le librerie mancanti.

## Passaggi successivi {#next-steps}

È disponibile un ambiente AEM Forms Document Services funzionante. È possibile utilizzare document services tramite:

* [Flussi di lavoro incentrati sui moduli su OSGi](/help/forms/using/aem-forms-workflow.md)
* [Cartelle controllate](/help/forms/using/watched-folder-in-aem-forms.md)
* [API di Document Services](/help/forms/using/aem-document-services-programmatically.md)
