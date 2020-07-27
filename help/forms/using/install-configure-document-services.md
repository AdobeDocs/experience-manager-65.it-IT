---
title: Installazione e configurazione di document services
seo-title: Installazione e configurazione di document services
description: Installare AEM Forms document services per creare, assemblare, distribuire, archiviare documenti PDF, aggiungere firme digitali per limitare l'accesso ai documenti e decodificare moduli con codice a barre.
seo-description: Installare AEM Forms document services per creare, assemblare, distribuire, archiviare documenti PDF, aggiungere firme digitali per limitare l'accesso ai documenti e decodificare moduli con codice a barre.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '4295'
ht-degree: 1%

---


# Installazione e configurazione di document services {#installing-and-configuring-document-services}

I AEM Forms forniscono una serie di servizi OSGi per eseguire diverse operazioni a livello di documento, ad esempio servizi per creare, assemblare, distribuire e archiviare documenti PDF, aggiungere firme digitali per limitare l&#39;accesso ai documenti e decodificare moduli con codice a barre. Questi servizi sono inclusi nel pacchetto del componente aggiuntivo AEM Forms. Collettivamente, questi servizi sono noti come document services. Di seguito è riportato l&#39;elenco delle funzionalità principali e dei servizi documenti disponibili:

* **Servizio Assembler:** Consente di combinare, ridisporre e ampliare i documenti PDF e XDP e di ottenere informazioni sui documenti PDF. Consente inoltre di convertire e convalidare documenti PDF in PDF/A standard, di trasformare PDF forms, moduli XML e PDF forms in PDF/A-1b, PDF/A-2b e PDFA/A-3b. Per ulteriori informazioni, consulta [Assembler Service](/help/forms/using/assembler-service.md).

* **Servizio ConvertPDF:** Consente di convertire i documenti PDF in file PostScript o di immagini (JPEG, JPEG 2000, PNG e TIFF). Per ulteriori informazioni, vedere [ConvertPDF Service](/help/forms/using/using-convertpdf-service.md).

* **Servizio Moduli codici a barre:** Consente di estrarre dati da immagini elettroniche di codici a barre. Il servizio accetta file TIFF e PDF che includono uno o più codici a barre come input e li estrae. Per ulteriori informazioni, vedere [Servizio](/help/forms/using/using-barcoded-forms-service.md)Moduli codici a barre.

* **Servizio DocAssurance:** Consente di cifrare e decrittografare i documenti, ampliare le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi e aggiungere firme digitali ai documenti. Il servizio Doc Assurance contiene tre servizi: firma, cifratura e estensione del lettore. Per ulteriori informazioni, vedere [DocAssurance Service](/help/forms/using/overview-aem-document-services.md).

* **Servizio di cifratura:** Consente di cifrare e decrittografare i documenti. Quando un documento viene crittografato, il relativo contenuto diventa illeggibile. Un utente autorizzato può decifrare il documento per ottenere l&#39;accesso ai contenuti. Per ulteriori informazioni, vedere [Servizio](/help/forms/using/overview-aem-document-services.md#encryption-service)di cifratura.

* **Servizio Forms:** Consente di creare applicazioni client per l&#39;acquisizione dei dati interattive per la convalida, l&#39;elaborazione, la trasformazione e la distribuzione di moduli che vengono generalmente creati in Forms Designer. Il servizio Forms esegue il rendering di qualsiasi struttura del modulo che si sviluppa in documenti PDF. Per ulteriori informazioni, vedere [Forms Service](/help/forms/using/forms-service.md).

* **Servizio di output:** Consente di creare documenti in diversi formati, tra cui PDF, formati per stampanti laser e formati per stampanti di etichette. I formati delle stampanti laser sono PostScript e PCL (Printer Control Language). Per ulteriori informazioni, vedere [Output Service](/help/forms/using/output-service.md).

* **servizio PDF Generator:** Il servizio PDF Generator fornisce API per la conversione dei formati di file nativi in PDF. Consente inoltre di convertire i file PDF in altri formati e di ottimizzare le dimensioni dei documenti PDF. Per ulteriori informazioni, vedere [PDF Generator Service](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Servizio Reader Extension:** Consente alla vostra azienda di condividere facilmente i documenti PDF interattivi estendendo le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi. Il servizio attiva funzioni non disponibili all&#39;apertura di un documento PDF tramite Adobe Reader, ad esempio l&#39;aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento. Per ulteriori informazioni, vedere [Reader Extension Service](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Servizio firma:** Consente di lavorare con firme digitali e documenti sul server AEM. Ad esempio, il servizio Signature è in genere utilizzato nelle situazioni seguenti:

   * Il server AEM certifica un modulo prima che venga inviato all&#39;utente per l&#39;apertura mediante Acrobat o Adobe Reader.
   * Il server AEM convalida una firma aggiunta a un modulo utilizzando Acrobat o Adobe Reader.
   * Il server AEM firma un modulo per conto di un notaio pubblico.

   Il servizio firma accede ai certificati e alle credenziali memorizzate nell&#39;archivio certificati attendibili. Per ulteriori informazioni, vedere [Servizio](/help/forms/using/aem-document-services-programmatically.md)firme.

AEM Forms è una potente piattaforma di classe enterprise e document services è solo una delle funzionalità dei AEM Forms. Per l&#39;elenco completo delle funzionalità, consultate [Introduzione ai AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

Il pacchetto aggiuntivo AEM Forms è un’applicazione distribuita in AEM. In genere, per eseguire AEM Forms document services è necessaria una sola istanza di AEM (creazione o pubblicazione). Per eseguire AEM Forms document services è consigliabile utilizzare la topologia seguente. Per informazioni dettagliate sulle topologie, consultate Topologie di [architettura e distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Topologie di architettura e implementazione per AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Anche se i AEM Forms consentono di configurare ed eseguire tutte le funzionalità da un singolo server, è necessario eseguire la pianificazione della capacità, il bilanciamento del carico e configurare server dedicati per capacità specifiche in un ambiente di produzione. Ad esempio, per un ambiente che utilizza il servizio PDF Generator per convertire migliaia di pagine al giorno e più moduli adattivi per l&#39;acquisizione dei dati, impostare server AEM Forms separati per il servizio PDF Generator e le funzionalità dei moduli adattivi. Consente di fornire prestazioni ottimali e di ridimensionare i server indipendentemente l&#39;uno dall&#39;altro.

## Requisiti di sistema {#system-requirements}

Prima di iniziare a installare e configurare AEM Forms document services, assicurarsi che:

* L&#39;infrastruttura hardware e software è già in funzione. Per un elenco dettagliato di hardware e software supportati, consultate i requisiti [tecnici](/help/sites-deploying/technical-requirements.md).

* Il percorso di installazione dell’istanza AEM non contiene spazi bianchi.
* Un’istanza di AEM è attiva e in esecuzione. Nella terminologia di AEM, per &quot;istanza&quot; si intende una copia di AEM in esecuzione su un server in modalità di creazione o pubblicazione. In genere, per eseguire AEM Forms document services è necessaria una sola istanza di AEM (creazione o pubblicazione):

   * **Autore**: Un’istanza di AEM utilizzata per creare, caricare e modificare i contenuti e per amministrare il sito Web. Quando il contenuto è pronto per essere live, viene replicato nell’istanza di pubblicazione.
   * **Pubblica**: Un’istanza di AEM che trasmette il contenuto pubblicato al pubblico su Internet o su una rete interna.

* I requisiti di memoria sono soddisfatti. Il pacchetto del componente aggiuntivo AEM Forms richiede:

   * 15 GB di spazio temporaneo per le installazioni basate su Microsoft Windows.
   * 6 GB di spazio temporaneo per le installazioni basate su UNIX.

* Sono installati i software client necessari per il generatore PDF per eseguire la conversione in Microsoft Windows e Linux:

   * **Microsoft Windows**: Installare [Microsoft](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)Office o [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux**: Installare [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* In Microsoft Windows, PDF Generator supporta i percorsi di conversione WebKit, Acrobat WebCapture e PhantomJS per convertire i file HTML in documenti PDF.
>* Nei sistemi operativi basati su UNIX, PDF Generator supporta i percorsi di conversione WebKit e PhantomJS per convertire i file HTML in documenti PDF.

>



### Requisiti aggiuntivi per il sistema operativo basato su UNIX {#extrarequirements}

Se si utilizza il sistema operativo basato su UNIX, installare i seguenti pacchetti dal supporto di installazione del rispettivo sistema operativo:

<table> 
 <tbody> 
  <tr> 
   <td> 
    <ul> 
     <li>espatriato</li> 
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
     <li>libuuid</li> 
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
     <li>libXrendering</li> 
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

* **(Solo** PDF Generator) Installate la versione a 32 bit delle librerie libcurl, libcrypto e libssl e create i seguenti simboli. I symlinks fanno riferimento all&#39;ultima versione delle rispettive librerie:

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(Solo Generatore PDF)** Il servizio PDF Generator supporta le route WebKit e PhantomJS per convertire i file HTML in documenti PDF. Per abilitare la conversione per la route PhantomJS, installate le librerie a 64 bit elencate di seguito. In genere, queste librerie sono già installate. Se manca una libreria, installatela manualmente:

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

Le configurazioni elencate nella sezione delle configurazioni di pre-installazione sono applicabili solo al servizio PDF Generator. Se non si configura il servizio PDF Generator, è possibile ignorare la sezione relativa alla configurazione di pre-installazione.

### Installare Adobe Acrobat e applicazioni di terze parti {#install-adobe-acrobat-and-third-party-applications}

Se utilizzate il servizio PDF Generator per convertire in documenti PDF formati di file nativi quali Microsoft Word, Microsoft Excel, Microsoft PowerPoint, OpenOffice, WordPerfect X7 e Adobe Acrobat, accertatevi che tali applicazioni siano installate nel server AEM Forms.

>[!NOTE]
>
>* Adobe Acrobat, Microsoft Word, Excel e Powerpoint sono disponibili solo per Microsoft Windows. Se si utilizza il sistema operativo basato su UNIX, installare OpenOffice per convertire file di testo RTF e file di Microsoft Office supportati in documenti PDF.
>* Tutte le finestre di dialogo visualizzate dopo l&#39;installazione di Adobe Acrobat e del software di terze parti per tutti gli utenti configurati per l&#39;utilizzo del servizio PDF Generator vengono disattivate.
>* Avviare il software installato almeno una volta. Chiudete tutte le finestre di dialogo per tutti gli utenti configurati per l&#39;utilizzo del servizio PDF Generator.

>



Dopo aver installato Acrobat, aprite Microsoft Word. Nella **scheda** Acrobat, fare clic **su Crea PDF** e convertire un file .doc o .docx disponibile sul computer in un documento PDF. Se la conversione ha esito positivo, i AEM Forms sono pronti per utilizzare Acrobat con il servizio PDF Generator.

### Impostazione delle variabili di ambiente {#setup-environment-variables}

Impostate le variabili di ambiente per i kit di sviluppo Java a 32 bit e a 64 bit, le applicazioni di terze parti e Adobe Acrobat. Le variabili di ambiente devono contenere il percorso assoluto dell&#39;eseguibile utilizzato per avviare l&#39;applicazione corrispondente, ad esempio la tabella seguente elenca le variabili di ambiente per alcune applicazioni:

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
>* Tutte le variabili di ambiente e i rispettivi percorsi sono con distinzione tra maiuscole e minuscole.
>* JAVA_HOME, JAVA_HOME_32 e Acrobat_PATH (solo Windows) sono variabili di ambiente obbligatorie.
>* La variabile di ambiente OpenOffice_PATH è impostata sulla cartella di installazione invece del percorso dell&#39;eseguibile.
>* Non impostare variabili di ambiente per applicazioni di Microsoft Office quali Word, PowerPoint, Excel e Project o per AutoCAD. Se queste applicazioni sono installate sul server, il servizio Genera PDF avvia automaticamente queste applicazioni.
>* Sulle piattaforme basate su UNIX, installate OpenOffice come /root. Se OpenOffice non è installato come root, il servizio PDF Generator non riesce a convertire i documenti OpenOffice in documenti PDF. Se è necessario installare ed eseguire OpenOffice come utente non principale, fornire i diritti di sudo all&#39;utente non principale.
>* Se si utilizza OpenOffice su una piattaforma basata su UNIX, eseguire il comando seguente per impostare la variabile del percorso:

>
>  
`export OpenOffice_PATH=/opt/openoffice.org4`

### (Solo per IBM WebSphere) Configurare il provider socket SSL IBM {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Per configurare il provider socket SSL IBM, effettuate le seguenti operazioni:

1. Create una copia del file java.security. Il percorso predefinito del file è `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Aprite il file java.security copiato per la modifica.
1. Modificate i socket SSL predefiniti per utilizzare le fabbriche JSSE2 invece delle fabbriche IBM WebSphere predefinite:

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

1. Per consentire al server AEM Forms di utilizzare il file java.security aggiornato, mentre si avvia il server AEM Forms, aggiungere il seguente argomento Java:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Solo Windows) Configurare il servizio di installazione dell&#39;inchiostro e della scrittura a mano {#configure-install-ink-and-handwriting-service}

Se si esegue Microsoft Windows Server, configurare il servizio di scrittura a penna e a mano. Il servizio è necessario per aprire i file di Microsoft PowerPoint che utilizzano le funzionalità di collegamento di Microsoft Office:

1. Aprire Server Manager. Fare clic sull&#39;icona **[!UICONTROL Server Manager]** nella barra di avvio rapido.
1. Fate clic su **[!UICONTROL Aggiungi funzioni]** nel menu **[!UICONTROL Funzioni]** . Selezionare la casella di controllo Servizi **[!UICONTROL di]** inchiostro e grafia.
1. **[!UICONTROL Selezionare la finestra di dialogo Funzioni]** con **[!UICONTROL Ink and Handwrite Services]** selezionato. Fate clic su **[!UICONTROL Installa]** e il servizio è installato.

### (Solo Windows) Configurare le impostazioni dei blocchi di file per Microsoft Office {#configure-the-file-block-settings-for-microsoft-office}

Modificate le impostazioni del centro protezione di Microsoft Office per abilitare il servizio PDF Generator per convertire i file creati con versioni precedenti di Microsoft Office.

1. Aprite un&#39;applicazione di Microsoft Office. Ad esempio, Microsoft Word. Passare a **[!UICONTROL File]**> **[!UICONTROL Opzioni]**. Viene visualizzata la finestra di dialogo delle opzioni.

1. Fare clic su Centro **** protezione e quindi su Impostazioni **[!UICONTROL centro]** protezione.
1. Nelle impostazioni **[!UICONTROL Centro]** protezione fare clic su Impostazioni **[!UICONTROL blocco]** file.
1. Nell&#39;elenco Tipo **[!UICONTROL di]** file, deselezionare **[!UICONTROL Apri]** per il tipo di file che il servizio PDF Generator deve poter convertire in documenti PDF.

### (Solo Windows) Concedere il privilegio di sostituzione di un token a livello di processo {#grant-the-replace-a-process-level-token-privilege}

L&#39;account utente utilizzato per avviare il server applicazione richiede il **privilegio di sostituzione di un token** a livello di processo. Per impostazione predefinita, l&#39;account di sistema locale dispone del privilegio **Sostituisci token** a livello di processo. Per i server in esecuzione con un utente del gruppo Amministratori locali, il privilegio deve essere concesso esplicitamente. Per concedere il privilegio, effettuate le seguenti operazioni:

1. Aprire l&#39;Editor Criteri di gruppo per Microsoft Windows. Per aprire l&#39;Editor Criteri di gruppo, fare clic su **[!UICONTROL Start]**, digitare **gpedit.msc** nella casella Avvia ricerca, quindi fare clic su Editor **[!UICONTROL criteri di]** gruppo.
1. Andate a Criteri **[!UICONTROL computer]** locali > Configurazione **** computer > Impostazioni **** Windows > Impostazioni **** protezione > Criteri **** **** **** locali > Assegnazione diritti utente e modificate il criterio relativo al token a livello di processo, quindi includete il gruppo Amministratori.
1. Aggiungete l&#39;utente alla voce Replace a Process Level Token (Sostituisci token a livello di processo).

### (Solo Windows) Abilitare il servizio PDF Generator per i non amministratori {#enable-the-pdf-generator-service-for-non-administrators}

È possibile consentire a un utente non amministratore di utilizzare il servizio PDF Generator. Normalmente, solo gli utenti con privilegi amministrativi possono utilizzare il servizio:

1. Creare una variabile di ambiente, PDFG_NON_ADMIN_ENABLED.
1. Impostate il valore della variabile di ambiente su TRUE.
1. Riavviate l&#39;istanza AEM Forms.

### (Solo Windows) Disattiva Controllo account utente (UAC) {#disable-user-account-control-uac}

1. Per accedere a System Configuration Utility, accedete a **[!UICONTROL Start > Esegui]** , quindi immettete **[!UICONTROL MSCONFIG]**.
1. Fare clic sulla scheda **[!UICONTROL Strumenti]** , scorrere verso il basso e selezionare **[!UICONTROL Modifica impostazioni]** controllo dell&#39;account utente. Fate clic su **[!UICONTROL Avvia]** per eseguire il comando in una nuova finestra.
1. Regolare il cursore sul livello Mai notifica. Al termine, chiudete la finestra del comando e chiudete la finestra Configurazione di sistema.
1. Verificate che l&#39;impostazione del Registro di sistema per l&#39;account utente sia impostata su 0 (zero). Effettuate le seguenti operazioni per verificare:

   1. Microsoft consiglia di eseguire il backup del Registro di sistema prima di modificarlo. Per i passaggi dettagliati, vedere [Procedura per eseguire il backup e ripristinare il Registro di sistema in Windows](https://support.microsoft.com/en-us/help/322756).
   1. Aprire l&#39;editor del Registro di sistema di Microsoft Windows. Per aprire l&#39;editor del Registro di sistema, selezionate Start > Esegui, digitate regedit e fate clic su OK.
   1. Accedi a `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Assicurarsi che il valore EnableLUA sia impostato su 0 (zero).
   1. Assicurarsi che il valore **EnableLUA** sia impostato su 0 (zero). Se il valore non è 0, modificare il valore in 0. Chiudere l&#39;editor del Registro di sistema.

1. Riavviate il computer.

### (Solo Windows) Disattivazione del servizio di segnalazione errori {#disable-error-reporting-service}

Durante la conversione di un documento in PDF tramite il servizio PDF Generator in Windows Server, talvolta Windows Server segnala che l&#39;eseguibile ha rilevato un problema e deve essere chiuso. Tuttavia, non ha alcun impatto sulla conversione PDF così come continua in background.

Per evitare di ricevere l&#39;errore, potete disattivare la segnalazione degli errori di Windows. Per ulteriori informazioni sulla disattivazione della segnalazione degli errori, vedere [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Solo Windows) Configurare la conversione da HTML a PDF {#configure-html-to-pdf-conversion}

Il servizio PDF Generator fornisce percorsi o metodi WebKit, WebCapture e PhantomJS per convertire i file HTML in documenti PDF. In Windows, per abilitare la conversione per i percorsi WebKit e Acrobat WebCapture, copiare il font Unicode nella directory %windir%\fonts.

>[!NOTE]
>
>Ogni volta che installate i nuovi font nella cartella dei font, riavviate l&#39;istanza AEM Forms.

### (Solo piattaforme basate su UNIX) Configurazioni aggiuntive per la conversione da HTML a PDF  {#extra-configurations-for-html-to-pdf-conversion}

Sulle piattaforme basate su UNIX, il servizio PDF Generator supporta le route WebKit e PhantomJS per convertire i file HTML in documenti PDF. Per abilitare la conversione da HTML a PDF, eseguite le seguenti configurazioni, in base al percorso di conversione desiderato:

### (Solo piattaforme basate su UNIX) Abilitare il supporto per i font Unicode (solo WebKit) {#enable-support-for-unicode-fonts-webkit-only}

Copiate il font Unicode in una delle seguenti directory, a seconda delle necessità del sistema in uso:

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris)

>[!NOTE]
>
>* Su RedHat Enterprise Linux 6.x e versioni successive, i font del corriere non sono disponibili. Per installare i font del corriere, scaricate l&#39;archivio font-ibm-type1-1.0.3.zip. Estraete l&#39;archivio in /usr/share/fonts. Create un collegamento simbolico da /usr/share/X11/fonts a /usr/share/fonts.
>* Eliminate tutti i file .lst della cache dei font dalle directory Html2PdfSvc/bin e /usr/share/fonts.
>* Verificate che le directory /usr/lib/X11/fonts e /usr/share/fonts esistano. Se le directory non esistono, utilizzate il comando ln per creare un collegamento simbolico da /usr/share/X11/fonts a /usr/lib/X11/fonts e un altro collegamento simbolico da /usr/share/fonts a /usr/share/X11/fonts. Verificate inoltre che i font del corriere siano disponibili in /usr/lib/X11/fonts.
>* Verificate che tutti i font (Unicode e non Unicode) siano disponibili nella directory /usr/share/fonts o /usr/share/X11/fonts.
>* Quando si esegue il servizio PDF Generator come utente non principale, fornire all&#39;utente non principale l&#39;accesso in lettura e scrittura a tutte le directory dei font.
>* Ogni volta che installate i nuovi font nella cartella dei font, riavviate l&#39;istanza AEM Forms.

>



## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

Il pacchetto aggiuntivo AEM Forms è un’applicazione distribuita in AEM. Il pacchetto contiene AEM Forms Document Services e altre funzionalità AEM Forms. Per installare il pacchetto, effettuate le seguenti operazioni:

1. Apri distribuzione [](https://experience.adobe.com/downloads)software. È necessario un Adobe ID  per accedere a Distribuzione software.
1. Toccate **[!UICONTROL Adobe Experience Manager]** disponibile nel menu dell&#39;intestazione.
1. Nella sezione **[!UICONTROL Filtri]** :
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]** .
   2. Selezionate la versione e digitate il tipo di pacchetto. Potete anche utilizzare l&#39;opzione Download **[!UICONTROL di]** ricerca per filtrare i risultati.
1. Toccate il nome del pacchetto applicabile al sistema operativo in uso, selezionate **[!UICONTROL Accetta termini]** EULA e toccate **[!UICONTROL Scarica]**.
1. Aprite [Package Manager](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Select the package and click **[!UICONTROL Install]**.

   Potete anche scaricare il pacchetto tramite il collegamento diretto elencato nell&#39;articolo delle release [](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html) AEM Forms.

1. Dopo l&#39;installazione del pacchetto, viene richiesto di riavviare l&#39;istanza di AEM. **Non arrestare immediatamente il server.** Prima di arrestare il server AEM Forms, attendere che i messaggi ServiceEvent REGISTERED e ServiceEvent UNREGISTERED non vengano visualizzati nel file `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log e il registro sia stabile.

## Configurazioni post-installazione {#post-installation-configurations}

### Configurare la delega di avvio per le librerie RSA/BouncyCastle  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Arrestate l’istanza AEM. Andate alla directory di installazione di [AEM]\crx-quickstart\conf\ folder. Aprite il file sling.properties per la modifica.

   Se utilizzate `[AEM installation directory]\crx-quickstart\bin\start.bat` per avviare un’istanza di AEM, modificate le proprietà sling.properties che si trovano in `[AEM_root]\crx-quickstart\`.

1. Aggiungete le seguenti proprietà al file sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. (Solo AIX) Aggiungete le seguenti proprietà al file sling.properties:

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Salvate e chiudete il file.

### Configurazione del servizio di gestione dei font  {#configuring-the-font-manager-service}

1. Accedete ad [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) come amministratore.
1. Individuate e aprite il servizio **[!UICONTROL CQ-DAM-Handler-Gibson Font Manager]** . Specificate il percorso delle directory Font di sistema, Font server Adobe e Font cliente. Fai clic su **[!UICONTROL Salva]**.

   >[!NOTE]
   >
   >Il diritto dell&#39;utente di utilizzare i font forniti da soggetti diversi da Adobe è disciplinato dai contratti di licenza forniti da tali soggetti con tali font e non è coperto dalla licenza di utilizzo del software Adobe. Adobe consiglia di rivedere e assicurarsi che l&#39;utente sia conforme a tutti i contratti di licenza applicabili non Adobe prima di utilizzare font non Adobe con il software Adobe, in particolare per quanto riguarda l&#39;uso dei font in un ambiente server.
   > Quando installate i nuovi font nella cartella dei font, riavviate l&#39;istanza dei AEM Forms.

### Configurare un account utente locale per eseguire il servizio PDF Generator  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Per eseguire il servizio PDF Generator è necessario un account utente locale. Per i passaggi necessari per creare un utente locale, consultate [Creare un account utente in Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) o [creare un account utente nelle piattaforme](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html)basate su UNIX.

1. Aprire la pagina [AEM Forms PDF Generator Configuration](http://localhost:4502/libs/fd/pdfg/config/ui.html) .

1. Nella scheda Account **** utente, immettete le credenziali di un account utente locale e fate clic su **[!UICONTROL Invia]**. Se viene richiesto da Microsoft Windows, consentite l&#39;accesso all&#39;utente. Una volta aggiunto correttamente, l&#39;utente configurato viene visualizzato nella sezione **[!UICONTROL Account]** utente nella scheda Account **** utente.

### Configurare le impostazioni di timeout {#configure-the-time-out-settings}

1. In [AEM Configuration Manager](http://localhost:4502/system/console/configMgr), individuate e aprite il servizio **[!UICONTROL Jacorb ORB Provider]** .

   Aggiungi quanto segue al campo **[!UICONTROL Custom Properties.name]** e fai clic su **[!UICONTROL Save (Salva]**). Imposta il timeout della risposta in sospeso (noto anche come timeout del client CORBA) su 600 secondi.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Accedi all’istanza di creazione di AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Moduli]** > **[!UICONTROL Configura generatore]** PDF. L’URL predefinito è http://localhost:4502/libs/fd/pdfg/config/ui.html.

   Aprite la scheda Configurazione **** generale e modificate il valore dei seguenti campi per l’ambiente:

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
   <td>270 seconds<br /> </td> 
  </tr> 
  <tr> 
   <td>Scansione di pulizia PDFG in secondi</td> 
   <td>Il numero di secondi necessari per eseguire le operazioni post-conversione.<br /> </td> 
   <td>3600 secondi</td> 
  </tr> 
  <tr> 
   <td>Scadenza processo in secondi</td> 
   <td>Durata per la quale il servizio PDF Generator può eseguire una conversione. Verificare che il valore dei secondi di scadenza del processo sia maggiore del valore PDFG Cleanup Scan Seconds.</td> 
   <td>7200 secondi</td> 
  </tr> 
 </tbody> 
</table>

### (Solo Windows) Configurare Acrobat per il servizio PDF Generator {#configure-acrobat-for-the-pdf-generator-service}

In Microsoft Windows, il servizio PDF Generator utilizza Adobe Acrobat per convertire i formati file supportati in un documento PDF. Per configurare Adobe Acrobat per il servizio PDF Generator, effettuate le seguenti operazioni:

1. Aprite Acrobat e selezionate **[!UICONTROL Modifica]**> **[!UICONTROL Preferenze]**> **[!UICONTROL Updater]**. In Cerca aggiornamenti, deselezionate **[!UICONTROL Installa automaticamente gli aggiornamenti]** e fate clic su **[!UICONTROL OK]**. Chiudere Acrobat.
1. Fare doppio clic su un documento PDF nel sistema. Quando Acrobat viene avviato per la prima volta, vengono visualizzate le finestre di dialogo per l&#39;accesso, la schermata introduttiva e l&#39;EULA. Visualizza queste finestre di dialogo per tutti gli utenti configurati per l&#39;utilizzo di PDF Generator.
1. Eseguire il file batch dell&#39;utility PDF Generator per configurare Acrobat per il servizio PDF Generator:

   1. Aprite [AEM Package Manager](http://localhost:4502/crx/packmgr/index.jsp) e scaricate il `adobe-aemfd-pdfg-common-pkg-[version].zip` file dal gestore pacchetti.
   1. Decomprimete il file .zip scaricato. Aprite il prompt dei comandi con privilegi amministrativi.
   1. Andate alla `[extracted-zip-file]\jcr_root\etc\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\scripts` directory. Eseguire il seguente file batch:

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat è configurato per essere eseguito con il servizio PDF Generator.

1. Per convalidare l&#39;installazione di Acrobat, eseguite SRT (System Readiness Tool). Lo strumento verifica se il computer è configurato correttamente per eseguire le conversioni di PDF Generator e genera un rapporto nel percorso specificato:

   1. Aprite il prompt dei comandi. Passate alla `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\etc\fd\ pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\srt` cartella. Eseguire il comando seguente dal prompt dei comandi:

      `cscript SystemReadinessTool.vbs [Path_of_reports_folder] en`

      >[!NOTE]
      >
      >Se System Readiness Tool segnala che il file pdfgen.api non è disponibile nella cartella dei plug-in di acrobat, copiate il file pdfgen.api dalla `[extracted-adobe-aemfd-pdfg-common-pkg]\plugins\x86_win32` directory alla `[Acrobat_root]\Acrobat\plug_ins` directory.

   1. Accedi a `[Path_of_reports_folder]`. Aprite il file SystemReadinessTool.html. Verifica il rapporto e risolvi i problemi indicati.

### (Solo Windows) Configurare la route principale per la conversione da HTML a PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

Il servizio PDF Generator consente di convertire i file HTML in documenti PDF in diversi modi: Webkit, Acrobat WebCapture (solo Windows) e PhantomJS. Adobe consiglia di utilizzare la route PhantomJS perché dispone della capacità di gestire il contenuto dinamico e non ha dipendenze in librerie a 32 bit, JDK a 32 bit o non richiede font aggiuntivi. Inoltre, la route PhantomJS non richiede l&#39;accesso di tipo sudo o root per eseguire la conversione.

La route principale predefinita per la conversione da HTML a PDF è Webkit. Per modificare il percorso di conversione:

1. Nell’istanza di creazione di AEM, andate a **[!UICONTROL Strumenti]**> **[!UICONTROL Moduli]**> **[!UICONTROL Configura PDF Generator]**.

1. Nella scheda Configurazione **** generale, selezionare il percorso di conversione preferito dall&#39;elenco a discesa Route **[!UICONTROL principale per conversioni]** da HTML a PDF.

### Inizializza archivio trust globale {#intialize-global-trust-store}

Utilizzando la funzione Trust Store Management, è possibile importare, modificare ed eliminare i certificati affidabili sul server per la convalida delle firme digitali e l&#39;autenticazione tramite certificato. È possibile importare ed esportare qualsiasi numero di certificati. Dopo l&#39;importazione di un certificato, è possibile modificare le impostazioni di attendibilità e il tipo di archivio attendibili. Per inizializzare uno store attendibile, effettuare le seguenti operazioni:

1. Accedete all&#39;istanza AEM Forms come amministratore.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Trust Store]**.
1. Fare clic su **[!UICONTROL Crea TrustStore]**. Impostate la password e toccate **[!UICONTROL Salva]**.

### Configurare i certificati per il servizio di estensione e crittografia di Reader {#set-up-certificates-for-reader-extension-and-encryption-service}

Il servizio DocAssurance può applicare diritti di utilizzo ai documenti PDF. Per applicare diritti di utilizzo ai documenti PDF, configurate i certificati.

Prima di impostare i certificati, assicurarsi di disporre di:

* File di certificato (.pfx).

* Password chiave privata fornita con il certificato.

* Alias chiave privata. È possibile eseguire il comando Java keytool per visualizzare l&#39;alias della chiave privata:
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Password del file del Keystore. Se si utilizza il certificato Adobe Reader Extensions, la password del file Keystore è sempre la stessa della password della chiave privata.

Per configurare i certificati, effettuate le seguenti operazioni:

1. Accedete all&#39;istanza AEM Author come amministratore. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**.
1. Fate clic sul campo del **[!UICONTROL nome]** dell’account utente. Viene visualizzata la pagina **[!UICONTROL Modifica impostazioni]** utente. Nell&#39;istanza AEM Author, i certificati risiedono in un KeyStore. Se non avete già creato un KeyStore in precedenza, fate clic su **[!UICONTROL Create KeyStore]** e impostate una nuova password per KeyStore. Se il server contiene già un KeyStore, ignora questo passaggio.  Se si utilizza il certificato Adobe Reader Extensions, la password del file Keystore è sempre la stessa della password della chiave privata.
1. Nella pagina **[!UICONTROL Modifica impostazioni]** utente, selezionate la scheda **[!UICONTROL KeyStore]** . Espandete l&#39;opzione **[!UICONTROL Aggiungi chiave privata dal file]** archivio chiavi e fornite un alias. L&#39;alias viene utilizzato per eseguire l&#39;operazione Reader Extensions.
1. Per caricare il file del certificato, fate clic su **[!UICONTROL Seleziona file]** archivio chiavi e caricate un file &lt;nomefile>.pfx.

   Aggiungete ai rispettivi campi la password **[!UICONTROL archivio]** chiavi, la password **[!UICONTROL chiave]** privata e l’alias **[!UICONTROL chiave]** privata associato al certificato. Fate clic su **[!UICONTROL Invia]**.

   >[!NOTE]
   >
   >* Nell&#39;ambiente di produzione, sostituite le credenziali di valutazione con le credenziali di produzione. Prima di aggiornare le credenziali scadute o di valutazione, assicurarsi di eliminare le vecchie credenziali di Reader Extensions.


1. Fate clic su **[!UICONTROL Salva e chiudi]** nella pagina **[!UICONTROL Modifica impostazioni]** utente.

### Abilita AES-256 {#enable-aes}

Per utilizzare la cifratura AES 256 per i file PDF, è necessario ottenere e installare i file JCE (Java Cryptography Extension) Unlimited Strense Jurisdizione Policy. Sostituite i file local_policy.jar e US_export_policy.jar nella cartella jre/lib/security. Ad esempio, se utilizzate Sun JDK, copiate i file scaricati nella `[JAVA_HOME]/jre/lib/security` cartella.

Il servizio Assembler dipende dal servizio Reader Extensions, dal servizio Signature, dal servizio Forms e dal servizio Output. Effettuate le seguenti operazioni per verificare che i servizi richiesti siano operativi:

1. Accedete all&#39;URL `https://'[server]:[port]'/system/console/bundles` come amministratore.
1. Cercate il servizio seguente e verificate che i servizi siano operativi:

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
   <td>Reader Extensions Service</td> 
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

* La conversione da HTML a PDF non riesce se un file di input compresso contiene file HTML con caratteri a doppio byte nei nomi dei file. Per evitare questo problema, non utilizzate caratteri a doppio byte per denominare i file HTML.

* Nei sistemi operativi basati su UNIX, effettuate le seguenti operazioni per individuare eventuali librerie mancanti:

1. Accedi a `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Eseguite il comando seguente per elencare tutte le librerie che PhantomJS richiede per la conversione da HTML a PDF.

   `ldd phantomjs`

   Eseguite il comando seguente per elencare le librerie mancanti.

   `ldd phantomjs | grep not`

1. Installate manualmente le librerie mancanti.

## Passaggi successivi {#next-steps}

È presente un ambiente Document Services AEM Forms funzionante. È possibile utilizzare document services tramite:

* [Flussi di lavoro incentrati sui moduli in OSGi](/help/forms/using/aem-forms-workflow.md)
* [Cartelle controllate](/help/forms/using/watched-folder-in-aem-forms.md)
* [API di Document Services](/help/forms/using/aem-document-services-programmatically.md)

