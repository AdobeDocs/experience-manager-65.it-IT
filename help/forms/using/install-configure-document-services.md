---
title: Installazione e configurazione dei servizi documentali
description: Installa AEM Forms Document Services per creare, assemblare, distribuire, archiviare documenti PDF, aggiungere firme digitali per limitare l’accesso ai documenti e decodificare Forms in codice a barre.
topic-tags: installing
role: Admin, User, Developer
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
source-git-commit: 5dbdce2d8e558e6bf26c6713fd44d58038d38152
workflow-type: tm+mt
source-wordcount: '5724'
ht-degree: 1%

---

# Installazione e configurazione dei servizi documentali {#installing-and-configuring-document-services}

AEM Forms fornisce un set di servizi OSGi per eseguire diverse operazioni a livello di documento, ad esempio servizi per creare, assemblare, distribuire e archiviare documenti PDF, aggiungere firme digitali per limitare l’accesso ai documenti e decodificare Forms in codice a barre. Questi servizi sono inclusi nel pacchetto del componente aggiuntivo AEM Forms. Nel complesso, questi servizi sono noti come servizi di documentazione. Di seguito è riportato un elenco dei servizi documentali disponibili e delle relative principali funzionalità:

* **Servizio assemblatore:** consente di combinare, ridisporre e integrare documenti PDF e XDP e di ottenere informazioni sui documenti PDF. Aiuta anche a convertire e convalidare i documenti PDF in PDF/A standard, trasforma PDF forms, moduli XML e PDF forms in PDF/A-1b, PDF/A-2b e PDFA/A-3b. Per ulteriori informazioni, vedere [Servizio assemblatore](/help/forms/using/assembler-service.md).

* **Converti servizio PDF:** Consente di convertire i documenti di PDF in file PostScript o di immagine (JPEG, JPEG 2000, PNG e TIFF). Per ulteriori informazioni, vedere [ConvertPDF Service](/help/forms/using/using-convertpdf-service.md).

* **Servizio Forms in codice a barre:** consente di estrarre dati da immagini elettroniche di codici a barre. Il servizio accetta file TIFF e PDF che includono uno o più codici a barre come input ed estrae i dati del codice a barre. Per ulteriori informazioni, vedere [Servizio Forms in codice a barre](/help/forms/using/using-barcoded-forms-service.md).

* **Servizio DocAssurance:** Consente di crittografare e decrittografare documenti, estendere le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi e aggiungere firme digitali ai documenti. Il servizio Doc Assurance contiene tre servizi: firma, crittografia ed estensione Reader. Per ulteriori informazioni, vedere [Servizio DocAssurance](/help/forms/using/overview-aem-document-services.md).

* **Servizio di crittografia:** consente di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l’accesso al relativo contenuto. Per ulteriori informazioni, vedere [Servizio di crittografia](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Servizio Forms:** consente di creare applicazioni client di acquisizione dati interattive che convalidano, elaborano, trasformano e distribuiscono moduli generalmente creati in Forms Designer. Il servizio Forms esegue il rendering di qualsiasi struttura di modulo sviluppata in documenti PDF. Per ulteriori informazioni, vedere [Servizio Forms](/help/forms/using/forms-service.md).

* **Servizio di output:** consente di creare documenti in formati diversi, inclusi PDF, formati di stampanti laser e formati di stampanti di etichette. I formati delle stampanti laser sono PostScript e Printer Control Language (PCL). Per ulteriori informazioni, vedere [Servizio di output](/help/forms/using/output-service.md).

* **Servizio PDF Generator:** Il servizio PDF Generator fornisce API per la conversione di formati di file nativi in PDF. Converte inoltre PDF in altri formati di file e ottimizza le dimensioni dei documenti PDF. Per ulteriori informazioni, vedere [Servizio PDF Generator](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Servizio di estensione Reader:** consente all&#39;organizzazione di condividere facilmente i documenti PDF interattivi estendendo la funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi. Il servizio attiva funzionalità non disponibili quando un documento di PDF viene aperto mediante Adobe Reader, ad esempio l&#39;aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento. Per ulteriori informazioni, vedere [Servizio di estensione Reader](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Servizio di firma:** consente di utilizzare le firme digitali e i documenti nel server AEM. Ad esempio, il servizio di firma viene utilizzato in genere nelle situazioni seguenti:

   * Il server AEM certifica un modulo prima che venga inviato a un utente per l’apertura tramite Acrobat o Adobe Reader.
   * Il server AEM convalida una firma aggiunta a un modulo tramite Acrobat o Adobe Reader.
   * Il server AEM firma un modulo per conto di un notaio pubblico.

  Il servizio di firma accede ai certificati e alle credenziali archiviati nell&#39;archivio fonti attendibili. Per ulteriori informazioni, vedere [Servizio firma](/help/forms/using/aem-document-services-programmatically.md).

AEM Forms è una potente piattaforma di classe enterprise e document services è solo una delle funzionalità di AEM Forms. Per un elenco completo delle funzionalità, vedere [Introduzione all AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

AEM Forms pacchetto aggiuntivo è un applicazione distribuito in AEM. In genere, è necessario un solo AEM istanza (autore o pubblicare) per eseguire AEM Forms Document Services. Per l&#39;esecuzione AEM Forms Document Services si consiglia la topologia seguente. Per informazioni dettagliate sulle topologie, vedere [Architettura e topologie di distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Architettura e topologie di distribuzione per AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Anche se AEM Forms consente di impostare ed eseguire tutte le funzionalità da un singolo server, è necessario eseguire la pianificazione della capacità, il bilanciamento del carico e la configurazione di server dedicati per funzionalità specifiche in un ambiente di produzione. Ad esempio, per un ambiente che utilizza il servizio PDF Generator per convertire migliaia di pagine al giorno e più moduli adattivi per l’acquisizione dei dati, configura server AEM Forms separati per il servizio PDF Generator e le funzionalità dei moduli adattivi. Consente di fornire prestazioni ottimali e scalare i server in modo indipendente l&#39;uno dall&#39;altro.

## Requisiti di sistema {#system-requirements}

Prima di iniziare l’installazione e la configurazione dei servizi documentali di AEM Forms, assicurati:

* Infrastruttura hardware e software già esistente. Per un elenco dettagliato di hardware e software supportati, vedere [requisiti tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell’istanza di AEM non contiene spazi vuoti.
* Un’istanza di AEM è attiva e in esecuzione. Nella terminologia di AEM, per &quot;istanza&quot; si intende una copia di AEM in esecuzione su un server in modalità di authoring o pubblicazione. In genere, per eseguire i servizi documentali di AEM Forms è necessaria una sola istanza di AEM (authoring o pubblicazione):

   * **Autore**: istanza di AEM utilizzata per creare, caricare e modificare contenuti e amministrare il sito Web. Quando il contenuto è pronto per essere pubblicato, viene replicato nell’istanza di pubblicazione.
   * **Pubblicazione**: istanza di AEM che fornisce il contenuto pubblicato al pubblico tramite Internet o una rete interna.

* I requisiti di memoria sono soddisfatti. Il pacchetto del componente aggiuntivo AEM Forms richiede:

   * 15 GB di spazio temporaneo per le installazioni basate su Microsoft® Windows.
   * 6 GB di spazio temporaneo per installazioni basate su UNIX.

* Il software client necessario affinché il generatore PDF esegua la conversione su Microsoft® Windows e Linux® è installato:

   * **Microsoft® Windows**: installa [Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) o [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux®**: installa [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* In Microsoft® Windows, PDF Generator supporta percorsi di conversione WebKit, Acrobat WebCapture e WebToPDF per convertire i file HTML in documenti PDF.
>* Nei sistemi operativi basati su UNIX, PDF Generator supporta le route di conversione WebKit e WebToPDF per convertire i file HTML in documenti PDF.
>

### Requisiti aggiuntivi per sistemi operativi basati su UNIX {#extrarequirements}

Se si utilizza un sistema operativo basato su UNIX, installare i seguenti pacchetti a 32 bit dal supporto di installazione del rispettivo sistema operativo:
<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>expat</li>
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
     <li>libuuide</li>
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

* **(solo PDF Generator**) Installa la versione a 32 bit delle librerie libcurl, libcrypto e libssl e crea i symlink seguenti. I collegamenti simbolici puntano alla versione più recente delle rispettive librerie:

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(solo PDF Generator)** Il servizio PDF Generator supporta le route WebKit e WebToPDF per la conversione di file HTML in documenti PDF. Per abilitare la conversione per la route WebToPDF, installare le librerie a 64 bit elencate di seguito. In genere, queste librerie sono già installate. Se manca una libreria, installala manualmente:

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

Le configurazioni elencate nella sezione configurazioni di preinstallazione sono applicabili solo al servizio PDF Generator. Se non configuri il servizio PDF Generator, puoi saltare la sezione di configurazione della preinstallazione.

### Installare applicazioni Adobe Acrobat e di terze parti {#install-adobe-acrobat-and-third-party-applications}

Se si intende utilizzare il servizio PDF Generator per convertire i formati di file nativi come Microsoft® Word, Microsoft® Excel, Microsoft® PowerPoint, OpenOffice, WordPerfect X7 e Adobe Acrobat in documenti PDF, assicurarsi che tali applicazioni siano installate nel server AEM Forms.

>[!NOTE]
>
>* Se il tuo server AEM Forms si trova in un ambiente offline o protetto e Internet non è disponibile per attivare Adobe Acrobat, consulta [Attivazione offline](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) per le istruzioni su come attivare tali istanze di Adobe Acrobat.
>* Adobe Acrobat, Microsoft® Word, Excel e Powerpoint sono disponibili solo per Microsoft® Windows. Se si utilizza il sistema operativo basato su UNIX, installare OpenOffice per convertire i file RTF e i file Microsoft® Office supportati in documenti PDF.
>* Chiudi tutte le finestre di dialogo visualizzate dopo l’installazione di Adobe Acrobat e del software di terze parti per tutti gli utenti configurati per l’utilizzo del servizio PDF Generator.
>* Avviare tutto il software installato almeno una volta. Ignora tutte le finestre di dialogo per tutti gli utenti configurati per utilizzare il servizio PDF Generator.
>* [Controllare la data di scadenza dei numeri di serie di Adobe Acrobat](https://helpx.adobe.com/enterprise/kb/volume-license-expiration-check.html) e impostare una data per l&#39;aggiornamento della licenza oppure [migrare il numero di serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) in base alla data di scadenza.

Dopo aver installato Acrobat, aprire Microsoft® Word. Nella scheda **Acrobat**, fai clic su **Crea PDF** e converti un file .doc o .docx disponibile nel computer in un documento PDF. Se la conversione ha esito positivo, AEM Forms è pronto a utilizzare Acrobat con il servizio PDF Generator.

### Configurare le variabili di ambiente {#setup-environment-variables}

Imposta le variabili di ambiente per Java Development Kit a 64 bit, applicazioni di terze parti e Adobe Acrobat. Le variabili di ambiente devono contenere il percorso assoluto dell&#39;eseguibile utilizzato per avviare l&#39;applicazione corrispondente. Ad esempio, nella tabella seguente sono elencate le variabili di ambiente per alcune applicazioni:

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
   <td><p>File C:\Program (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>Blocco note</strong></p> </td>
   <td><p>Notepad_PATH</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice</strong></p> </td>
   <td><p>OpenOffice_PATH</p> </td>
   <td><p>File C:\Program (x86)\OpenOffice 4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Tutte le variabili di ambiente e i rispettivi percorsi fanno distinzione tra maiuscole e minuscole.
>* JAVA_HOME e Acrobat_PATH (solo Windows) sono variabili di ambiente obbligatorie.
>* La variabile di ambiente OpenOffice_PATH è impostata sulla cartella di installazione anziché sul percorso dell&#39;eseguibile.
>* Non impostare variabili di ambiente per applicazioni Microsoft® Office come Word, PowerPoint, Excel e Project o per AutoCAD. Se queste applicazioni sono installate sul server, il servizio Generate PDF avvia automaticamente queste applicazioni.
>* Sulle piattaforme basate su UNIX, installare OpenOffice come /root. Se OpenOffice non è installato come radice, il servizio PDF Generator non riesce a convertire i documenti OpenOffice in documenti PDF. Se è necessario installare ed eseguire OpenOffice come utente non root, specificare i diritti sudo per l&#39;utente non root.
>* Se si utilizza OpenOffice su una piattaforma basata su UNIX, eseguire il comando seguente per impostare la variabile di percorso:\
> `export OpenOffice_PATH=/opt/openoffice.org4`
>* Sulle piattaforme basate su SUSE® Linux® (SLES 15 SP6 o versioni successive), effettuare le seguenti operazioni per configurare OpenOffice:
>     * Installa l&#39;ultima variante a 32 bit disponibile di `OpenOffice 4.1.x` in una directory come `/opt/openoffice4`.
>     * Impostare la variabile di ambiente `OpenOffice_PATH` in modo che punti a questa posizione. Ad esempio: `OpenOffice_PATH=/opt/openoffice4`.
>     * Assicurati che la `OpenOffice_PATH` variabile sia impostata globalmente (ad esempio, utilizzando `/etc/profile` o l&#39;equivalente specifico del sistema) in modo che sia disponibile per tutti gli utenti al momento dell&#39;login.

### (Solo per IBM® WebSphere®) Configurazione del provider socket SSL IBM® {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Per configurare il provider di socket SSL IBM®, effettua le seguenti operazioni:

1. Crea una copia del file java.security. Il percorso predefinito del file è `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Apri il file java.security copiato per la modifica.
1. Modificare le factory socket SSL predefinite per utilizzare le factory JSSE2 anziché le factory IBM® WebSphere® predefinite:

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

1. Per consentire ad AEM Forms Server di utilizzare il file java.security aggiornato all’avvio del server AEM Forms, aggiungi il seguente argomento java:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Solo Windows) Configurare le impostazioni di blocco file per Microsoft® Office {#configure-the-file-block-settings-for-microsoft-office}

Modificare le impostazioni del Centro protezione di Microsoft® Office per consentire al servizio PDF Generator di convertire i file creati con versioni precedenti di Microsoft® Office.

1. Aprire un&#39;applicazione di Microsoft® Office. Microsoft® Word. Passa a **[!UICONTROL File]**> **[!UICONTROL Opzioni]**. Viene visualizzata la finestra di dialogo delle opzioni.

1. Fare clic su **[!UICONTROL Centro protezione]** e quindi su **[!UICONTROL Impostazioni Centro protezione]**.
1. Nelle **[!UICONTROL impostazioni Centro protezione]**, fare clic su **[!UICONTROL Impostazioni blocco file]**.
1. Nell&#39;elenco **[!UICONTROL Tipo File]** , deselezionare **[!UICONTROL Apri]** per il tipo di file che il servizio PDF Generator deve consentire di convertire ai documenti PDF.

### (Solo Windows) Concedere all&#39;Sostituisci un privilegio di token a livello di processo {#grant-the-replace-a-process-level-token-privilege}

Il utente account utilizzato per avviare il server applicazione richiede il **Sostituisci un privilegio di token** a livello di processo. Per impostazione predefinita, il account di sistema locale dispone della **Sostituisci un privilegio di token** a livello di processo. Per i server in esecuzione con un utente del gruppo Administrators locale, il privilegio deve essere concesso in modo esplicito. Esegui i seguenti passaggi per concedere il privilegio:

1. Aprire l&#39;Editor Criteri di gruppo per Microsoft® Windows. Per aprire l&#39;Editor Criteri di gruppo, fare clic su **[!UICONTROL Inizio]**, digitare **gpedit.msc** nella casella Avvia ricerca, quindi fare clic su **[!UICONTROL Editor Criteri di gruppo]**.
1. Passa a **[!UICONTROL Criteri computer locale]** > **[!UICONTROL Configurazione computer]** > **[!UICONTROL Impostazioni di Windows]** > **[!UICONTROL Impostazioni protezione]** > **[!UICONTROL Criteri locali]** > **[!UICONTROL Assegnazione diritti utente]** e modifica il criterio **[!UICONTROL Sostituisci un token a livello di processo]** e includi il gruppo Administrators.
1. Aggiungere l&#39;utente alla voce Sostituisci token a livello di processo.

>[!NOTE]
>
> Come indicato in precedenza, se il server AEM è in esecuzione come servizio con l&#39;account LocalSystem (LSA), non è necessario assegnare esplicitamente questo privilegio a un utente.

### (Solo Windows) Abilita il servizio PDF Generator per i non amministratori {#enable-the-pdf-generator-service-for-non-administrators}

È possibile consentire a un utente non amministratore di utilizzare il servizio PDF Generator. Normalmente, solo gli utenti con privilegi amministrativi possono utilizzare il servizio:

1. Creare una variabile di ambiente, PDFG_NON_ADMIN_ENABLED.
1. Imposta il valore della variabile di ambiente su TRUE.
1. Riavvia l’istanza di AEM Forms.

>[!NOTE]
>
> Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.

### (Solo Windows) Disabilita Controllo account utente {#disable-user-account-control-uac}

1. Per accedere all&#39;Utilità Configurazione di sistema, passare a **[!UICONTROL Start > Esegui]** e quindi immettere **[!UICONTROL MSCONFIG]**.
1. Fai clic sulla scheda **[!UICONTROL Strumenti]**, scorri verso il basso e seleziona **[!UICONTROL Modifica impostazioni Controllo dell&#39;account utente]**. Fare clic su **[!UICONTROL Avvia]** per eseguire il comando in una nuova finestra.
1. Regolare il dispositivo di scorrimento al livello di notifica Mai. Al termine, chiudere la finestra dei comandi e la finestra Configurazione di sistema.
1. Verificare che l&#39;impostazione del Registro di sistema per Controllo account utente sia impostata su 0 (zero). Per verificare, effettua le seguenti operazioni:

   1. Microsoft® consiglia di eseguire il backup del Registro di sistema prima di modificarlo. Per i passaggi dettagliati, vedere [Eseguire il backup e il ripristino del Registro di sistema in Windows](https://support.microsoft.com/en-us/help/322756).
   1. Aprire l&#39;editor del Registro di sistema di Microsoft® Windows. Per aprire l&#39;editor del Registro di sistema, passare a Start > Esegui, digitare regedit e fare clic su OK.
   1. Passa a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Assicurarsi che il valore di EnableLUA sia impostato su 0 (zero).
   1. Assicurarsi che il valore di **EnableLUA** sia impostato su 0 (zero). Se il valore non è 0, modificare il valore in 0. Chiudi l’editor del Registro di sistema.

1. Riavvia il computer.

### (Solo Windows) Disabilita il servizio Segnalazione errori {#disable-error-reporting-service}

Durante la conversione di un documento in PDF utilizzando il servizio PDF Generator su Windows Server, occasionalmente, Windows Server segnala che l&#39;eseguibile ha rilevato un problema e deve chiudere. Tuttavia, non influisce sulla conversione PDF in quanto continua in background.

Per evitare di ricevere l&#39;errore, è possibile disattivare la segnalazione errori di Windows. Per ulteriori informazioni sulla disattivazione della segnalazione errori, consulta [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Solo Windows) Configura conversione da HTML a PDF {#configure-html-to-pdf-conversion}

Il servizio PDF Generator fornisce percorsi o metodi WebKit, WebCapture e WebToPDF per convertire i file HTML in documenti PDF. In Windows, per abilitare la conversione per le route WebKit e Acrobat WebCapture, copiare il carattere Unicode nella directory %windir%\fonts.

>[!NOTE]
>
>Ogni volta che si installano nuovi tipi di carattere nella cartella dei tipi di carattere, riavviare l&#39;istanza di AEM Forms.

### (Solo piattaforme basate su UNIX) Configurazioni aggiuntive per la conversione da HTML a PDF  {#extra-configurations-for-html-to-pdf-conversion}

Sulle piattaforme basate su UNIX, il servizio PDF Generator supporta le route WebKit e WebToPDF per convertire i file HTML in documenti PDF. Per abilitare la conversione da HTML a PDF, esegui le seguenti configurazioni, in base al percorso di conversione preferito:

### (Solo piattaforme basate su UNIX) Abilitazione del supporto per i caratteri Unicode (solo WebKit) {#enable-support-for-unicode-fonts-webkit-only}

Copiare il tipo di carattere Unicode in una delle seguenti directory, a seconda del sistema in uso:

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris™)

>[!NOTE]
>
>* Su Red Hat® Enterprise Linux® 6.x e versioni successive, i font per corriere non sono disponibili. Per installare i caratteri del corriere, scarica l’archivio font-ibm-type1-1.0.3.zip. Estrai l’archivio in /usr/share/fonts. Crea un collegamento simbolico da /usr/share/X11/fonts a /usr/share/fonts.
>* Eliminare tutti i file della cache dei caratteri .lst dalle directory Html2PdfSvc/bin e /usr/share/fonts.
>* Assicurati che siano presenti le directory /usr/lib/X11/fonts e /usr/share/fonts. Se le directory non esistono, utilizzare il comando ln per creare un collegamento simbolico da /usr/share/X11/fonts a /usr/lib/X11/fonts e un altro collegamento simbolico da /usr/share/fonts a /usr/share/X11/fonts. Assicurati inoltre che i font del corriere siano disponibili all’indirizzo /usr/lib/X11/fonts.
>* Assicurarsi che tutti i font (Unicode e non Unicode) siano disponibili nella directory /usr/share/fonts o /usr/share/X11/fonts.
>* Quando si esegue il servizio PDF Generator come utente non root, fornire all&#39;utente non root accesso in lettura e scrittura a tutte le directory dei font.
>* Ogni volta che si installano nuovi tipi di carattere nella cartella dei tipi di carattere, riavviare l&#39;istanza di AEM Forms.
>

## Installare il pacchetto del componente aggiuntivo AEM Forms {#install-aem-forms-add-on-package}

Il pacchetto del componente aggiuntivo AEM Forms è un’applicazione implementata in AEM. Il pacchetto contiene AEM Forms Document Services e altre funzionalità di AEM Forms. Per installare il pacchetto, effettua le seguenti operazioni:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibili nel menu dell&#39;intestazione.
1. **[!UICONTROL Nella sezione Filtri]**:
   1. Seleziona **[!UICONTROL Forms]** dall&#39;elenco a **[!UICONTROL discesa Soluzione]** .
   2. Seleziona la versione e digita per il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Cerca download]** per filtrare i risultati.
1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accetta termini EULA]** e selezionare **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Selezionare il pacchetto e fare clic su **[!UICONTROL Installa]**.

   Puoi scaricare il pacchetto anche tramite il collegamento diretto elencato nell&#39;articolo [Versioni di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

1. Dopo l’installazione del pacchetto, viene richiesto di riavviare l’istanza di AEM. **Non arrestare immediatamente il server.** Prima di arrestare AEM Forms Server, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano più visualizzati nel file `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log e che il log sia stabile.

## Configurazioni post-installazione {#post-installation-configurations}

### Configurare la delega di avvio per le librerie RSA/BouncyCastle  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Arresta l’istanza di AEM. Passare alla cartella [Directory di installazione di AEM]\crx-quickstart\conf\. Apri il file sling.properties per la modifica.

   Se utilizzi `[AEM installation directory]\crx-quickstart\bin\start.bat` per avviare un&#39;istanza di AEM, modifica il file sling.properties che si trova in `[AEM_root]\crx-quickstart\`.

1. Aggiungi le seguenti proprietà al file sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. Solo per AIX® Aggiungi le seguenti proprietà al file sling.properties:

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Salva e chiudi il file.

### Configurazione del servizio Gestione tipi di carattere  {#configuring-the-font-manager-service}

1. Accedi a [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) come amministratore.
1. Individua e apri il servizio **[!UICONTROL CQ-DAM-Handler-Gibson Font Manager]**. Specifica il percorso delle directory System Fonts, Adobe Server Fonts e Customer Fonts. Fai clic su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Il diritto di utilizzare i font forniti da terze parti diverse da Adobe è disciplinato dai contratti di licenza forniti da tali parti con tali font e non è coperto dalla licenza d’uso del software Adobe. Adobe consiglia di verificare e assicurarsi di rispettare tutti i contratti di licenza non Adobe applicabili prima di utilizzare font non Adobe con il software Adobe, in particolare per quanto riguarda l’utilizzo di font in un ambiente server.
   >Quando si installano nuovi tipi di carattere nella cartella dei tipi di carattere, riavviare l&#39;istanza di AEM Forms.
   >

### Configurare un account utente locale per eseguire il servizio PDF Generator  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Per eseguire il servizio PDF Generator è necessario un account utente locale. Per i passaggi per creare un utente locale, vedere [Creare un account utente in Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) o creare un account utente in piattaforme basate su UNIX.

1. Apri la pagina [Configurazione AEM Forms PDF Generator](http://localhost:4502/libs/fd/pdfg/config/ui.html).

1. Nella scheda **[!UICONTROL Account utente]**, fornisci le credenziali di un account utente locale e fai clic su **[!UICONTROL Invia]**. Se Microsoft® Windows richiede, consenti l’accesso all’utente. Se l&#39;aggiunta viene aggiunta, la utente configurata viene visualizzata nella **[!UICONTROL sezione Account utente]** utente della **[!UICONTROL scheda Account]** utente.

### Configurare le impostazioni di timeout {#configure-the-time-out-settings}

1. In [AEM configuration manager](http://localhost:4502/system/console/configMgr), individuare e aprire il **[!UICONTROL servizio Jacorb ORB Provider]** .

   Aggiungi quanto segue al campo **[!UICONTROL Proprietà personalizzate.name]** e fai clic su **[!UICONTROL Salva]**. Imposta il timeout della risposta in sospeso (noto anche come timeout del client CORBA) su 600 secondi.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Accedi all&#39;istanza di AEM Author e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Configura PDF Generator]**. URL predefinito: <http://localhost:4502/libs/fd/pdfg/config/ui.html>.

   Apri la scheda **[!UICONTROL Configurazione generale]** e modifica il valore dei campi seguenti per l&#39;ambiente:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descrizione</td>
   <td>Valore predefinito</td>
  </tr>
  <tr>
   <td>Timeout conversione server</td>
   <td>Una conversione PDFG rimane attiva per il numero di secondi definiti nel timeout di conversione server</td>
   <td>270 secondi<br /> </td>
  </tr>
  <tr>
   <td>Scansione di pulizia PDFG in secondi</td>
   <td>Numero di secondi necessari per eseguire le operazioni di conversione post.<br /> </td>
   <td>3600 secondi</td>
  </tr>
  <tr>
   <td>Scadenza processo in secondi</td>
   <td>Durata per la quale il servizio PDF Generator può eseguire una conversione. Assicurati che il valore dei secondi di scadenza del processo sia maggiore del valore dei secondi di analisi di pulizia PDFG.</td>
   <td>7200 secondi</td>
  </tr>
 </tbody>
</table>

### (Solo Windows) Configura Acrobat per il servizio PDF Generator {#configure-acrobat-for-the-pdf-generator-service}

In Microsoft® Windows, il servizio PDF Generator utilizza Adobe Acrobat per convertire i formati di file supportati in un documento PDF. Per configurare Adobe Acrobat per il servizio PDF Generator, effettua le seguenti operazioni:

1. Apri Acrobat e seleziona **[!UICONTROL Modifica]**> **[!UICONTROL Preferenze]**> **[!UICONTROL Aggiornamento]**. In Verifica aggiornamenti deselezionare **[!UICONTROL Installa automaticamente gli aggiornamenti]** e fare clic su **[!UICONTROL OK]**. Chiudi Acrobat.
1. Fare doppio clic su un documento di PDF nel sistema. Quando Acrobat viene avviato per la prima volta, vengono visualizzate le finestre di dialogo per l’accesso, la schermata di benvenuto e le condizioni di licenza. Chiudere queste finestre di dialogo per tutti gli utenti configurati per l&#39;utilizzo di PDF Generator.
1. Esegui il file batch dell’utility PDF Generator per configurare Acrobat per il servizio PDF Generator:

   1. Apri [Gestione pacchetti AEM](http://localhost:4502/crx/packmgr/index.jsp) e scarica il file `adobe-aemfd-pdfg-common-pkg-[version].zip` da Gestione pacchetti.
   1. Decomprimi il file .zip scaricato. Aprire il prompt dei comandi con privilegi amministrativi.
   1. Passa alla `[extracted-zip-file]\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\`
   1. Decomprimere il file `adobe-aemfd-pdfg-common-pkg-[version]`.
   1. Passare alla `[downloaded-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]` directory. Eseguire il seguente file batch:

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat è configurato per l&#39;esecuzione con il servizio PDF Generator.

1. Esegui [Strumento di preparazione al sistema (SRT)](#SRT) per convalidare l&#39;installazione di Acrobat.

### (Solo per Windows) Configura la route principale per la conversione da HTML a PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

Il servizio PDF Generator fornisce più percorsi per convertire i file HTML in documenti PDF: Webkit, Acrobat WebCapture (solo Windows) e WebToPDF. Adobe consiglia di utilizzare la route WebToPDF perché è in grado di gestire contenuti dinamici e non ha dipendenze da librerie a 32 bit o non richiede font aggiuntivi. Inoltre, la route WebToPDF non richiede l&#39;accesso sudo o root per eseguire la conversione.

La route principale predefinita per la conversione da HTML a PDF è Webkit. Per modificare il percorso di conversione:

1. Nell&#39;istanza Autore AEM, passa a **[!UICONTROL Strumenti]**> **[!UICONTROL Forms]**> **[!UICONTROL Configura PDF Generator]**.

1. Nella scheda **[!UICONTROL Configurazione generale]**, selezionare la route di conversione preferita dal menu a discesa **[!UICONTROL Route principale per conversioni da HTML a PDF]**.

### Inizializza archivio fonti attendibili globale {#intialize-global-trust-store}

Tramite la gestione dell&#39;archivio fonti attendibili è possibile importare, modificare ed eliminare certificati attendibili nel server per la convalida delle firme digitali e l&#39;autenticazione dei certificati. È possibile importare ed esportare un numero qualsiasi di certificati. Dopo l&#39;importazione di un certificato, è possibile modificare le impostazioni di attendibilità e il tipo di archivio fonti attendibili. Per inizializzare un archivio fonti attendibili, eseguire la procedura seguente:

1. Accedi all’istanza di AEM Forms come amministratore.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Archivio attendibile]**.
1. Fare clic su **[!UICONTROL Crea TrustStore]**. Imposta la password e seleziona **[!UICONTROL Salva]**.

### Configurazione dei certificati per il servizio di crittografia e l&#39;estensione di Reader {#set-up-certificates-for-reader-extension-and-encryption-service}

Il servizio DocAssurance può applicare i diritti di utilizzo ai documenti di PDF. Per applicare i diritti di utilizzo ai documenti di PDF, configura i certificati.

Prima di impostare i certificati, assicurati di disporre di:

* File di certificato (.pfx).

* Password della chiave privata fornita con il certificato.

* Alias chiave privata. Puoi eseguire il comando Java keytool per visualizzare l’alias della chiave privata:
  `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Password del file registro chiavi. Se utilizzi il certificato Reader Extensions di Adobe, la password del file Keystore è sempre la stessa della password della chiave privata.

Per configurare i certificati, effettua le seguenti operazioni:

1. Accedi all’istanza di AEM Author come amministratore. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
1. Fai clic sul campo **[!UICONTROL name]** dell&#39;account utente. Viene visualizzata la pagina **[!UICONTROL Modifica impostazioni utente]**. Nella AEM Autore istanza, i certificati risiedono in un registro chiavi. Se in precedenza non è stato creato un KeyStore, fare clic su **[!UICONTROL Crea KeyStore]** e impostare una nuova password per il KeyStore. Se il server contiene già un KeyStore, salta questo passaggio.  Se utilizzi il certificato Reader Extensions di Adobe Systems, il password del file dell&#39;archivio chiavi è sempre lo stesso di password a chiave privata.
1. Nella pagina **[!UICONTROL Modifica impostazioni utente]** selezionare la scheda **[!UICONTROL KeyStore]**. Espandere l&#39;opzione **[!UICONTROL Aggiungi chiave privata dal file dell&#39;archivio chiavi]** e specificare un alias. L’alias viene utilizzato per eseguire l’operazione Reader Extensions.
1. Per caricare il file del certificato, fare clic su **[!UICONTROL Seleziona file di archivio chiavi]** e caricare un file &lt;nomefile>.pfx.

   Aggiungi **[!UICONTROL Password archivio chiavi]**, **[!UICONTROL Password chiave privata]** e **[!UICONTROL Alias chiave privata]** associati al certificato ai rispettivi campi. Fai clic su **[!UICONTROL Invia]**.

   >[!NOTE]
   >
   >Nell’ambiente di produzione, sostituisci le credenziali di valutazione con le credenziali di produzione. Prima di aggiornare una credenziale scaduta o di valutazione, accertati di eliminare le vecchie credenziali delle estensioni Reader.

1. Fare clic su **[!UICONTROL Salva e chiudi]** nella pagina **[!UICONTROL Modifica impostazioni utente]**.

### Abilita AES-256 {#enable-aes}

Per utilizzare la crittografia AES 256 per i file PDF, è necessario ottenere e installare i file Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy. Sostituisci i file local_policy.jar e US_export_policy.jar nella cartella jre/lib/security. Ad esempio, se si utilizza Sun JDK, copiare i file scaricati nella cartella `[JAVA_HOME]/jre/lib/security`.

Il servizio Assembler dipende dal servizio Estensioni Reader, dal servizio Firma, dal servizio Forms e dal servizio Output. Esegui i passaggi seguenti per verificare che i servizi necessari siano attivi e in esecuzione:

1. Accedi a URL `https://'[server]:[port]'/system/console/bundles` come amministratore.
1. Search il servizio seguente e assicurati che i servizi siano attivi e funzionanti:

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

### (Solo Windows) Configura voce del Registro di sistema per Microsoft® Project {#configure-registry-entry-for-microsoft-project}

Dopo aver installato il componente aggiuntivo AEM Forms e Microsoft® Project sul computer, registrare una voce per Microsoft® Project nel percorso a 64 bit. Facilita l’esecuzione dei test di conversione da Project a PDFG. Di seguito sono riportati i passaggi che descrivono la procedura per la voce del Registro di sistema:

1. Aprire l&#39;editor del Registro di sistema di Microsoft® Windows (regedit). Per aprire l&#39;editor del Registro di sistema, scegliere Start > Esegui, digitare regedit e fare clic su OK.
1. Passare a `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Adobe\Acrobat PDFMaker\<version>\Office\SupportedApp`, creare un nuovo **Registro di sistema Valore binario** e rinominarlo **Progetto**.
1. Modificare il valore dei dati del Registro di sistema binario creato su 01 e fare clic su OK.
1. Chiudere la voce del Registro di sistema.


## Problemi noti e risoluzione dei problemi {#known-issues-and-troubleshooting}

* La conversione da HTML a PDF non riesce se un file di input compresso contiene file HTML con caratteri a doppio byte nei nomi dei file. Per evitare questo problema, non utilizzare caratteri a doppio byte per la denominazione dei file HTML.

* Nei sistemi operativi basati su UNIX, effettuare le seguenti operazioni per trovare eventuali librerie mancanti:

1. Accedi a `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Eseguire il comando seguente per elencare tutte le librerie necessarie per la conversione da HTML a PDF.

   `ldd phantomjs`

   Esegui il comando seguente per elencare le librerie mancanti.

   `ldd phantomjs | grep not`

1. Installa manualmente le librerie mancanti.

## Strumento di preparazione al sistema (SRT) {#SRT}

Lo strumento [Preparazione sistema](#srt-configuration) verifica se il computer è configurato correttamente per eseguire conversioni PDF Generator. Lo strumento genera il report nel percorso specificato. Per eseguire lo strumento:

1. Apri il prompt dei comandi. Passare alla cartella `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools`.

1. Esegui il comando seguente dal prompt dei comandi:

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   Il comando genera il report e crea anche il file srt_config.yaml. Puoi utilizzarlo per configurare le opzioni per lo strumento SRT. È facoltativo configurare le opzioni per lo strumento SRT.

   >[!NOTE]
   >
   >* Se System Readiness Tool segnala che il file pdfgen.api non è disponibile nella cartella dei plug-in di Acrobat, copiare il file pdfgen.api dalla directory `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` alla directory `[Acrobat_root]\Acrobat\plug_ins`.

1. Passa a `[Path_of_reports_folder]`. Aprire il file SystemReadinessTool.html. Verifica il rapporto e correggi i problemi indicati.

### Configurazione delle opzioni per lo strumento SRT {#srt-configuration}

Potete utilizzare il file srt_config.yaml per configurare varie impostazioni per lo strumento SRT. Il formato del file è:

```shell
   # =================================================================
   # SRT Configuration
   # =================================================================
   #Note - follow correct format to avoid parsing failures
   #for example, <param name>:<space><param value> 
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

* **Impostazioni locali:** È un parametro obbligatorio. Supporta inglese (en), tedesco (de), francese (fr) e giapponese (ja). Il valore predefinito è en. Non ha alcun impatto sui servizi PDF Generator in esecuzione su AEM Forms su OSGi.
* **aemTempDir:** È un parametro facoltativo. Specifica il percorso di archiviazione temporanea di Adobe Experience Manager.
* **utenti:** Si tratta di un parametro facoltativo. È possibile specificare un utente per verificare se dispone delle autorizzazioni necessarie e dell&#39;accesso in lettura e scrittura alle directory necessarie per eseguire PDF Generator. Se non viene specificato alcun utente, i controlli specifici dell&#39;utente vengono ignorati e visualizzati come non riusciti nel rapporto.
* **outputDir:** Specificare il percorso in cui salvare il report SRT. La posizione di default è la directory di lavoro corrente dello strumento SRT.

## Risoluzione dei problemi

Se si verificano problemi anche dopo aver risolto tutti i problemi segnalati dallo strumento SRT, eseguire i controlli seguenti:

Prima di eseguire i controlli seguenti, verificare che [Strumento di preparazione al sistema](#SRT) non riporti alcun errore.

+++ Adobe Acrobat

* Verificare che sia installata solo la [versione supportata](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) di Microsoft® Office (32 bit) e Adobe Acrobat e che le finestre di dialogo di apertura siano annullate.
* Assicurati che Adobe Acrobat Update Service sia disabilitato.
* Verificare che il file batch [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) sia stato eseguito con privilegi di amministratore.
* Accertati che un utente PDF Generator sia aggiunto nell’interfaccia utente di configurazione di PDF.
* Assicurarsi che sia stata aggiunta l&#39;autorizzazione [Sostituisci un token a livello di processo](#grant-the-replace-a-process-level-token-privilege) per l&#39;utente PDF Generator.
* Verificare che Acrobat PDFMaker Office COM Addin sia abilitato per le applicazioni Microsoft Office.

+++

+++OpenOffice

**Microsoft® Windows**

* Assicurarsi che sia installata la versione[&#128279;](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) supportata a 32 bit di Microsoft Office e che le finestre di dialogo di apertura vengano annullate per tutte le applicazioni.
* Assicurarsi che nella interfaccia di configurazione PDF venga aggiunto un utente generatore di PDF.
* Assicurarsi che il utente PDF Generator sia membro del gruppo administrators e che il [Sostituisci sia impostato un privilegio token](#grant-the-replace-a-process-level-token-privilege) a livello di processo per il utente.
* Assicurati che l’utente sia configurato nell’interfaccia utente di PDF Generator ed esegua le azioni seguenti:
   1. Accedere a Microsoft® Windows con l&#39;utente PDF Generator.
   1. Aprire applicazioni Microsoft® Office o OpenOffice e annullare tutte le finestre di dialogo.
   1. Imposta Adobe PDF come stampante predefinita.
   1. Imposta Acrobat come programma predefinito per i file PDF.
   1. Eseguire la conversione manuale utilizzando le opzioni File > Stampa e Acrobat barra multifunzione nelle applicazioni di Microsoft Office e annullare tutte le finestre di dialogo.
   1. Terminare tutti i processi correlati alla conversione, ad esempio winword.exe, powerpoint.exe ed excel.exe.
   1. Riavvia il server AEM Forms.

**Linux®**

* Installa la [versione supportata](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) di OpenOffice. AEM Forms supporta sia le versioni a 32 bit che quelle a 64 bit. Dopo l&#39;installazione, aprire tutte le applicazioni OpenOffice, annullare tutte le finestre di dialogo e chiudere le applicazioni. Riaprire le applicazioni e assicurarsi che all&#39;apertura di un&#39;applicazione OpenOffice non venga visualizzata alcuna finestra di dialogo.

* Creare una variabile di ambiente `OpenOffice_PATH` e impostarla in modo che punti all&#39;installazione di OpenOffice è impostata nel profilo [console](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) o nel profilo dt (Device Tree).
* In caso di problemi durante l&#39;installazione di OpenOffice, verificare che siano disponibili le [librerie a 32 bit](#extrarequirements) necessarie per l&#39;installazione di OpenOffice.

+++

+++Problemi di conversione da HTML a PDF

* Assicurati che le directory dei font vengano aggiunte nell’interfaccia utente di configurazione di PDF Generator.

**Linux e Solaris (route di conversione WebToPDF)**

* Assicurati che la libreria a 32 bit sia disponibile (libicudata.so.42) per la conversione HTMLToPDF basata su Webkit e che le librerie a 64 bit (libicudata.so.42 siano disponibili per la conversione HTMLToPDF basata su WebToPDF.

* Eseguire il comando seguente per elencare le librerie mancanti per WebToPDF:

  ```
  ldd phantomjs | grep not
  ```

**Linux® e Solaris™ (route di conversione WebKit)**

* Verificare che le directory `/usr/lib/X11/fonts` e `/usr/share/fonts` esistano. Se le directory non esistono, creare un collegamento simbolico da `/usr/share/X11/fonts` a `/usr/lib/X11/fonts` e un altro da `/usr/share/fonts` a `/usr/share/X11/fonts`.

  ```
  ln -s /usr/share/fonts /usr/share/X11/fonts
  
  ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
  ```

* Assicurati che i font IBM siano copiati in usr/share/fonts.
* Assicurati che la correzione della vulnerabilità fantasma glibc sia disponibile sul computer. Utilizza il gestore di pacchetti predefinito per eseguire l’aggiornamento alla versione più recente di glibc. Include la correzione della vulnerabilità fantasma.
* Verifica che nel sistema siano installate le versioni più recenti delle librerie lib curl, libcrypto e libssl a 32 bit. Creare anche i symlink `/usr/lib/libcurl.so` (o libcurl.a per AIX®), `/usr/lib/libcrypto.so` (o libcrypto.a per AIX®) e `/usr/lib/libssl.so` (o libssl.a per AIX®) che puntano alle versioni più recenti (32 bit) delle rispettive librerie.

* Effettua le seguenti operazioni per il provider di socket SSL IBM®:
   1. Copiare il file java.security da `<WAS_Installed_JAVA>\jre\lib\security` in qualsiasi posizione sul server AEM Forms. La posizione predefinita è Posizione predefinita = `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.

   1. Modificare il file java.security nella posizione copiata e modificare le factory SSL Socket predefinite con factory JSSE2 (utilizzare factory JSSE2 invece di WebSphere®).

      Modificare i seguenti socket factory JSSE predefiniti:

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

* Verificare che Microsoft® Visual C++ 2012 x86 e Microsoft® Visual C++ 2013 x86 (32 bit) ridistribuibili siano installati in Windows.

+++

+++Errori di test di automazione

* Per Microsoft® Office e OpenOffice, eseguire almeno una conversione manualmente (come ogni utente) per assicurarsi che non venga visualizzata alcuna finestra di dialogo durante la conversione. Se viene visualizzata una finestra di dialogo, chiuderla. Durante la conversione automatica non dovrebbe essere visualizzata alcuna finestra di dialogo di questo tipo.

* Prima di eseguire l’automazione in un ambiente AEM Forms su OSGi, assicurati che il pacchetto di test sia installato e attivo.

+++

+++Errori di conversione di più utenti

* Verifica i registri del server per verificare se la conversione non riesce per un particolare utente.(Esplora processi consente di controllare il processo in esecuzione per utenti diversi)

* Assicurati che l’utente configurato per PDF Generator disponga dei diritti di amministratore locale.

* Assicurati che l’utente PDF Generator disponga delle autorizzazioni di lettura, scrittura ed esecuzione per gli utenti temporanei LC e PDFG.

* Per Microsoft® Office e OpenOffice, eseguire almeno una conversione manualmente (come ogni utente) per assicurarsi che non venga visualizzata alcuna finestra di dialogo durante la conversione. Se viene visualizzata una finestra di dialogo, chiuderla. Durante la conversione automatica non dovrebbe essere visualizzata alcuna finestra di dialogo di questo tipo.

* Esegui una conversione di esempio.

+++

+++Scadenza della licenza di Adobe Acrobat installata su AEM Forms Server

* Se si dispone di una licenza esistente di Adobe Acrobat ed è scaduta, [Scaricare l&#39;ultima versione di Adobe Application Manager](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html) e migrare il numero di serie. Prima di [eseguire la migrazione del numero](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) di serie.

   * Utilizzare i comandi seguenti per generare prov.xml e reserializzare l&#39;installazione esistente utilizzando il file prov.xml anziché i comandi forniti nell&#39;articolo numero di serie [migrazione del numero di serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

         &quot;
         
         adobe_prtk —tool=VolumeSerialize —generate —serial=&lt;serialnum> [—leid=&lt;LEID>] [—regsuppress=ss] [—eulasuppress] [—locales=elenco limitato di impostazioni locali in formato xx_XX o ALL>] [—provfile=&lt;Percorso assoluto a prov.xml>]
         
         &quot;
     
   * Serializzare il pacchetto con il volume (serializzare nuovamente l&#39;installazione esistente utilizzando il file prov.xml e il nuovo numero di serie): eseguire il comando seguente dalla cartella di installazione PRTK come amministratore per serializzare e attivare i pacchetti distribuiti sui computer client:

         &quot;
         adobe_prtk —tool=VolumeSerialize —provfile=C:\prov.xml -stream
         
         &quot;
     
* Per le installazioni su larga scala, utilizzare [Acrobat Customization Wizard](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) per rimuovere le versioni precedenti di Reader e Acrobat. Personalizzare il programma di installazione e distribuirlo in tutti i computer dell&#39;organizzazione.

+++

+++ AEM Forms Server è in un ambiente offline o protetto e Internet non è disponibile per attivare Acrobat.

* Puoi accedere a Internet entro 7 giorni dal primo lancio del prodotto Adobe per completare l’attivazione e la registrazione online oppure puoi utilizzare un dispositivo abilitato per Internet e il numero di serie del prodotto per completare la procedura. Per istruzioni dettagliate, vedere [Attivazione offline](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++

+++ Impossibile convertire file Word o Excel in PDF su Windows Server

Quando l&#39;utente cerca di convertire i file Word o Excel in PDF in Microsoft Windows Server, si verifica il seguente errore:

*Messaggio di errore del convertitore primario:
ALC-PDG-015-003-Impossibile aprire il file di input. Invia di nuovo il file o contatta l&#39;amministratore di sistema.*

Per risolvere il problema, vedere [Impossibile convertire il file Word o Excel in PDF su Windows Server](/help/forms/using/disable-uac-for-pdfgconfiguration.md).

+++

+++ Impossibile convertire i file Excel in PDF su Windows Server 2019

Quando si converte Microsoft Excel 2019 in PDF in Microsoft Windows Server 2019, è necessario verificare quanto segue:

* Durante l&#39;utilizzo del servizio PDF Generator, il computer non deve disporre di alcuna connessione remota attiva con il server AEM (sessione RDP di Windows).
* La stampante predefinita deve essere impostata su Adobe PDF.

  >[!NOTE]
  >* Per Apple macOS e Ubuntu OS non è necessario configurare le impostazioni sopra indicate.

+++

+++ Impossibile convertire i file XPS in PDF

Per risolvere il problema, [crea una chiave del Registro di sistema specifica della funzionalità in Windows](https://helpx.adobe.com/in/acrobat/kb/unable-convert-xps-to-pdfs.html).

+++


## Passaggi successivi {#next-steps}

È disponibile un ambiente AEM Forms Document Services funzionante. È possibile utilizzare i servizi documentali tramite:

* [Flussi di lavoro incentrati sul modulo su OSGi](/help/forms/using/aem-forms-workflow.md)
* [Cartelle controllate](/help/forms/using/watched-folder-in-aem-forms.md)
* [API di Document Services](/help/forms/using/aem-document-services-programmatically.md)
