---
title: Installazione e configurazione dei servizi documentali
description: Installa AEM Forms Document Services per creare, assemblare, distribuire, archiviare documenti PDF, aggiungere firme digitali per limitare l’accesso ai documenti e decodificare Forms in codice a barre.
topic-tags: installing
role: Admin, Developer
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
source-git-commit: b5e44b78659f0cb1b8b0025be30143b98c0bf8df
workflow-type: tm+mt
source-wordcount: '10051'
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

AEM Forms è una potente piattaforma di classe enterprise e i servizi di documentazione sono solo una delle funzionalità di AEM Forms. Per l&#39;elenco completo delle funzionalità, vedere [Introduzione ad AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia di distribuzione {#deployment-topology}

Il pacchetto del componente aggiuntivo AEM Forms è un’applicazione implementata in AEM. In genere, per eseguire i servizi documentali di AEM Forms è necessaria una sola istanza di AEM (authoring o pubblicazione). Per eseguire i servizi documentali di AEM Forms, si consiglia di utilizzare la topologia seguente. Per informazioni dettagliate sulle topologie, vedere [Architettura e topologie di distribuzione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

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
* (Solo per PDF Generator) Per abilitare la route WebKit nelle impostazioni RHEL 8 o RHEL 9, la libreria `nspr` a 32 bit potrebbe non essere disponibile per impostazione predefinita; installarla se non è presente.

* (Solo per PDF Generator) Se la conversione WebToPDF non riesce sul server Unix® con il seguente errore:

  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
quindi impostare la variabile di ambiente seguente e riavviare il server:
  `OPENSSL_CONF=/etc/ssl`

>[!NOTE]
>
> WebToPDF viene utilizzato anche dalla funzionalità Grafico nelle comunicazioni interattive. Pertanto, tutti i passaggi di configurazione indicati sopra per WebToPDF sono applicabili per garantire il corretto funzionamento della funzione Grafico.

## Configurazioni di preinstallazione {#preinstallationconfigurations}

Le configurazioni elencate nella sezione Configurazioni di preinstallazione sono applicabili solo al servizio PDF Generator. Se non configuri il servizio PDF Generator, puoi saltare la sezione di configurazione della preinstallazione.

### Installare applicazioni Adobe Acrobat e di terze parti {#install-adobe-acrobat-and-third-party-applications}

Se si intende utilizzare il servizio PDF Generator per convertire i formati di file nativi come Microsoft® Word, Microsoft® Excel, Microsoft® PowerPoint, OpenOffice e Adobe Acrobat in documenti PDF, assicurarsi che tali applicazioni siano installate nel server AEM Forms.

>[!NOTE]
>
><!-- * If your AEM Forms Server is in an offline or secure environment and internet is not available to activate Adobe Acrobat, see [Offline Activation](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) for instructions to activate such instances of Adobe Acrobat. -->
>* Adobe Acrobat, Microsoft® Word, Excel e Powerpoint sono disponibili solo per Microsoft® Windows. Se si utilizza il sistema operativo basato su UNIX, installare OpenOffice per convertire i file RTF e i file Microsoft® Office supportati in documenti PDF.
>* Chiudi tutte le finestre di dialogo visualizzate dopo l’installazione di Adobe Acrobat e del software di terze parti per tutti gli utenti configurati per l’utilizzo del servizio PDF Generator.
>* Avviare tutto il software installato almeno una volta. Ignora tutte le finestre di dialogo per tutti gli utenti configurati per utilizzare il servizio PDF Generator.
>* [Controllare la data di scadenza dei numeri di serie di Adobe Acrobat](https://helpx.adobe.com/enterprise/kb/volume-license-expiration-check.html) e impostare una data per l&#39;aggiornamento della licenza oppure [migrare il numero di serie](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) in base alla data di scadenza.

### Installare Adobe Acrobat Pro DC

#### Prerequisiti

Prima di installare Acrobat, controlla questi requisiti essenziali. Dovresti avere:

* Familiarità con [Adobe Admin Console](https://helpx.adobe.com/in/enterprise/admin-guide.html)
* Informazioni sull&#39;architettura di distribuzione di [AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)
* Privilegi amministrativi sia su Adobe Admin Console che sul server che esegue AEM Forms.
* Un utente con [accesso amministratore](https://helpx.adobe.com/in/enterprise/using/admin-roles.html) all&#39;Adobe [Admin Console](https://adminconsole.adobe.com). In genere, l’amministratore dell’organizzazione dispone già di un utente con accesso come amministratore. Puoi guardare questo [video informativo](https://www.youtube.com/watch?v=xO2T0I6SvsU&list=PLHRegP5ZOj7CpijZyD8pB9rIMJkvO6FnI&t=81s) per i passaggi necessari per aggiungere un amministratore.
* Un account utente con il ruolo [Amministratore distribuzione](https://helpx.adobe.com/in/enterprise/global-admin-console/manage-administrators.html) in Adobe Admin Console. Lo stesso [video di istruzioni](https://www.youtube.com/watch?v=xO2T0I6SvsU&list=PLHRegP5ZOj7CpijZyD8pB9rIMJkvO6FnI&t=81s) illustra come aggiungere un amministratore della distribuzione.
* Privilegi di amministratore locale sul computer che esegue AEM Forms
* Sistema operativo Windows a 64 bit
* Connessione Internet stabile per l&#39;attivazione della licenza
<!-- Backup solution for existing Acrobat settings
 Supported version of Adobe Acrobat (see [Adobe documentation](https://helpx.adobe.com/acrobat/kb/acrobat-dc-compatibility-with-windows-macos.html) for details) -->


#### Flusso di lavoro di implementazione e timeline

Il processo completo richiede in genere 1-2 ore, a seconda dell’ambiente:

| Passaggio | Tempo stimato | Prerequisiti |
|------|----------------|---------------|
| &#x200B;1. Creare un pacchetto FRL in Admin Console) | 15-20 minuti | [Accesso ad Admin Console](https://helpx.adobe.com/in/enterprise/admin-guide.html) |
| &#x200B;2. Concedere Le Autorizzazioni Di Download | 5-10 minuti | [Accesso ad Admin Console](https://helpx.adobe.com/in/enterprise/global-admin-console/manage-administrators.html) |
| &#x200B;3. Disinstallare Acrobat precedente | 10-15 minuti | Accesso amministratore del server |
| &#x200B;4. Scaricare e installare Adobe Acrobat Pro | 10-15 minuti | Accesso amministratore del server |
| &#x200B;5. Scaricare e distribuire il pacchetto FRL | 20-30 minuti | Accesso amministratore del server |
| &#x200B;6. Verifica dell’installazione | 5-10 minuti | Accesso al server |

<!-- ![Workflow diagram showing the FRL implementation process](/help/forms/using/assets/frl.svg) -->

**Scegliere Il Percorso Di Installazione**

Il processo di installazione di Adobe Acrobat Pro DC for Microsoft Office varia leggermente a seconda del tipo di licenza e dello scenario di installazione. Per assicurarti di seguire i passaggi corretti per il tuo ambiente specifico, seleziona la scheda che corrisponde alla configurazione:

* **Tipo di licenza**: vendita al dettaglio o Volume License
* **Tipo di distribuzione**: utente singolo o più utenti

Ogni scheda contiene istruzioni personalizzate ottimizzate per la configurazione specifica, che consentono di evitare problemi di configurazione e garantire la conformità alle licenze.

>[!BEGINTABS]

>[!TAB Licenza vendita al dettaglio - Utente singolo]

#### Impostazione delle licenze FRL (Feature Restricted Licensing) per Adobe Acrobat sul server AEM Forms

Questi passaggi presuppongono che tu disponga dei privilegi di amministratore necessari sia sul Adobe Admin Console che sul server che esegue AEM Forms.

##### Preparare il pacchetto FRL (Adobe Admin Console)

Questi passaggi devono essere eseguiti con l&#39;accesso *Amministratore di sistema* a Adobe Admin Console.

###### Passaggio 1: accedere a Adobe Admin Console

1. Apri un browser Web e passa a [Adobe Admin Console](https://adminconsole.adobe.com/)
1. Accedi utilizzando un account con *privilegi di amministratore di sistema*.
1. (Facoltativo) Se la tua organizzazione ha accesso a più organizzazioni IMS, utilizza l’opzione di selezione dell’organizzazione nell’angolo in alto a destra di Admin Console per scegliere l’organizzazione corretta. Nella maggior parte degli scenari dei clienti, questo sarebbe già impostato sul valore predefinito della tua organizzazione, in quanto gli utenti in genere hanno accesso solo alla propria organizzazione.

###### Passaggio 2: creare il pacchetto FRL

1. In Admin Console, passa alla scheda &quot;Pacchetti&quot;. Questo è un pacchetto Adobe Admin Console, non un pacchetto AEM.
1. Selezionare la scheda **Feature Restricted License** e fare clic sul pulsante **Inizia**. Accertarsi di selezionare il tipo di licenza corretto.
1. Nella schermata **Crea pacchetto**, configurare le impostazioni del pacchetto:

   | Impostazione | Valore consigliato | Note |
   |---------|-------------------|-------|
   | Metodo di attivazione | Offline | Opzione consigliata |
   | Diritto | Generazione PDF (PDFG) | Richiesto per la funzionalità AEM Forms PDF Generator |
   | Configura piattaforma | Windows a 64 bit | Apple macOS non è attualmente supportato |
   | Abilita locale | &quot;Usa lingua del sistema operativo&quot; | Impostazione predefinita |
   | Lingua | Lingua preferita | Per l’interfaccia di Acrobat |
   | Scegli le app - applicazioni disponibili | Mantieni Adobe Acrobat nelle applicazioni disponibili. Non spostare nell&#39;applicazione selezionata | Puoi [scaricare Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) dalla pagina Adobe Experience League al passaggio 6. |
   | Scegli app - applicazioni selezionate | Mantieni solo file di licenza nelle applicazioni selezionate | Impostazione predefinita per la distribuzione FRL |
   | Plug-in | Non apportare modifiche in questa schermata | |
   | Opzioni | Non apportare modifiche in questa schermata | |
   | Finalizza | Nome pacchetto: &quot;Acrobat FRL AEM Forms&quot; | Utilizza un nome descrittivo |

1. Fai clic su **Crea** per creare il pacchetto.

###### Passaggio 3: fornire le autorizzazioni per il download a un utente

Si consiglia di creare un account di servizio dedicato per la gestione dei pacchetti FRL. Se non disponi già di un account dedicato, puoi seguire [questo video di istruzioni](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) per scoprire come aggiungere un nuovo utente alla tua organizzazione Adobe.

Una volta che disponi dell’account appropriato, segui questi passaggi per concedere le autorizzazioni di download:

1. In Admin Console, passa alla scheda **Utenti**.
2. Individua o crea un account utente per concedere le autorizzazioni di download.
3. Fai clic sul nome dell’utente per aprire il suo profilo.
4. Fare clic sull&#39;icona accanto all&#39;utente **Modifica diritti amministratore**.
5. Assegna all&#39;utente il ruolo **Amministratore distribuzione**. Possono funzionare anche altri ruoli amministratore, ma il ruolo consigliato è Amministratore distribuzione. Fai clic su **Salva**.


##### Distribuire il pacchetto FRL (server AEM Forms)

I seguenti passaggi vengono eseguiti sul server AEM Forms, con i diritti di *amministratore locale* sul computer.

###### Passaggio 4: accedi al server che esegue AEM Forms come amministratore

Accedi al server che esegue AEM Forms utilizzando il metodo appropriato. Verificare di utilizzare un account con privilegi di amministratore locale per accedere al server.

###### Passaggio 5: disinstallare la versione precedente di Acrobat (se presente)

**Critico:** Prima di disinstallare, esegui il backup di impostazioni, profili o configurazioni Acrobat personalizzate.

1. Aprire il Pannello di controllo Campaign Windows.
2. Passa a **Impostazioni** e apri **App**.
3. Individua **Adobe Acrobat** nell&#39;elenco dei programmi installati
4. Seleziona **Disinstalla** e segui le istruzioni per rimuovere l&#39;applicazione. Se richiesto, riavviare il server
5. Verificare che tutte le versioni Classic del programma siano disinstallate. Se necessario, usa lo strumento [Adobe Acrobat Cleaner](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) per completare la rimozione.

###### Passaggio 6: Scaricare e installare Adobe Acrobat Pro

Dopo aver disinstallato la versione precedente, è necessario scaricare e installare una versione compatibile di Adobe Acrobat Pro:

1. Vai alla [pagina Download di Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Passa alla sezione **Programma di installazione di Acrobat Pro**.
3. Per l’utilizzo con AEM Forms PDF Generator, scarica il programma di installazione &quot;For Windows (32-Bit)&quot;, in quanto questa è la versione supportata con AEM Forms PDF Generator.
4. Seguire le istruzioni di installazione riportate nella pagina:
   * Estrai il file zip scaricato in una cartella sul computer
   * Passare al file Setup.exe (non eseguire il file Setup.exe dal file zip)
   * Fare doppio clic su Setup.exe per avviare l&#39;installazione
   * Seguire le istruzioni visualizzate sullo schermo per completare l&#39;installazione
5. Dopo l&#39;installazione, aprire Adobe Acrobat Pro e completare la configurazione iniziale eliminando le finestre di dialogo di benvenuto.
6. Verificare l&#39;installazione creando un PDF semplice.

###### Passaggio 7: scaricare il pacchetto FRL

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/) utilizzando l&#39;*account utente* a cui hai fornito le autorizzazioni di download al passaggio 3.
1. Passa alla scheda **Pacchetti**.
1. Individua il pacchetto FRL creato nel passaggio 2 (denominato &quot;Acrobat FRL AEM Forms&quot; o il nome del pacchetto personalizzato).
1. Fai clic su **Scarica** per scaricare il pacchetto sul server.

###### Passaggio 8: distribuire il pacchetto

1. **Estrarre il pacchetto:** Estrarre il contenuto del file ZIP scaricato in una directory sul server (ad esempio, `C:\AcrobatFRL`). Assicurati che la directory di estrazione sia facilmente accessibile.

2. **Apri prompt dei comandi come amministratore (Windows):** Fare clic con il pulsante destro del mouse sul pulsante Start e selezionare &quot;Prompt dei comandi (Admin)&quot; o &quot;Windows PowerShell (Admin)&quot;

3. **Accedere alla directory di estrazione:**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Esegui il comando di attivazione:**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Importante:**
   > * Sostituisci `<JSON_FILE_NAME>.json` con il nome file *exact* del file JSON nel pacchetto estratto.
   > * Il nome del file JSON distingue tra maiuscole e minuscole.
   > * Controllare il nome del file per eventuali errori di battitura.

   **Output previsto:**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **Nota:** Il processo di attivazione potrebbe richiedere circa 30 secondi.

5. **Informazioni sui parametri del comando:**

   | Parametro | Descrizione |
   |-----------|-------------|
   | `-p` | Specifica la piattaforma (rileva automaticamente il sistema operativo) |
   | `-i` | Indica allo strumento di installare e attivare la licenza |
   | `-f` | Specifica il percorso del file di licenza JSON |

###### Passaggio 9: verifica del servizio PDF Generator

Dopo aver completato tutti i processi, eseguire un test di azione rapida per confermare la validità dell&#39;installazione:

1. Aprire l’interfaccia di amministrazione di AEM Forms
2. Passare al servizio PDF Generator
3. Provare a convertire un semplice documento di Microsoft Office in PDF
4. Verifica che la conversione sia stata completata correttamente

#### Verifica della versione di Acrobat dopo l&#39;attivazione FRL

1. Apri Adobe Acrobat Pro DC sul server
2. Vai alla → Informazioni su Adobe Acrobat Pro DC
3. Verifica che il numero di versione corrisponda alla versione prevista
4. Conferma che lo stato della licenza sia attivato

>[!TAB Licenza Retail - Più utenti]

#### Impostazione delle licenze FRL (Feature Restricted Licensing) per Adobe Acrobat sul server AEM Forms

Questi passaggi presuppongono che tu disponga dei privilegi di amministratore necessari sia sul Adobe Admin Console che sul server che esegue AEM Forms.

##### Preparare il pacchetto FRL (Adobe Admin Console)

Questi passaggi devono essere eseguiti con l&#39;accesso *Amministratore di sistema* a Adobe Admin Console.

###### Passaggio 1: accedere a Adobe Admin Console

1. Apri un browser Web e passa a [Adobe Admin Console](https://adminconsole.adobe.com/)
1. Accedi utilizzando un account con *privilegi di amministratore di sistema*.
1. (Facoltativo) Se la tua organizzazione ha accesso a più organizzazioni IMS, utilizza l’opzione di selezione dell’organizzazione nell’angolo in alto a destra di Admin Console per scegliere l’organizzazione corretta. Nella maggior parte degli scenari dei clienti, questo sarebbe già impostato sul valore predefinito della tua organizzazione, in quanto gli utenti in genere hanno accesso solo alla propria organizzazione.

###### Passaggio 2: creare il pacchetto FRL

1. In Admin Console, passa alla scheda &quot;Pacchetti&quot;. Questo è un pacchetto Adobe Admin Console, non un pacchetto AEM.
1. Selezionare la scheda **Feature Restricted License** e fare clic sul pulsante **Inizia**. Accertarsi di selezionare il tipo di licenza corretto.
1. Nella schermata **Crea pacchetto**, configurare le impostazioni del pacchetto:

   | Impostazione | Valore consigliato | Note |
   |---------|-------------------|-------|
   | Metodo di attivazione | Offline | Opzione consigliata |
   | Diritto | Generazione PDF (PDFG) | Richiesto per la funzionalità AEM Forms PDF Generator |
   | Configura piattaforma | Windows a 64 bit | Apple macOS non è attualmente supportato |
   | Abilita locale | &quot;Usa lingua del sistema operativo&quot; | Impostazione predefinita |
   | Lingua | Lingua preferita | Per l’interfaccia di Acrobat |
   | Scegli le app - applicazioni disponibili | Mantieni Adobe Acrobat nelle applicazioni disponibili. Non spostare nell&#39;applicazione selezionata | Puoi [scaricare Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) dalla pagina Adobe Experience League al passaggio 6. |
   | Scegli app - applicazioni selezionate | Mantieni solo file di licenza nelle applicazioni selezionate | Impostazione predefinita per la distribuzione FRL |
   | Plug-in | Non apportare modifiche in questa schermata | |
   | Opzioni | Non apportare modifiche in questa schermata | |
   | Finalizza | Nome pacchetto: &quot;Acrobat FRL AEM Forms&quot; | Utilizza un nome descrittivo |

1. Fai clic su **Crea** per creare il pacchetto.

###### Passaggio 3: fornire le autorizzazioni per il download a un utente

Si consiglia di creare un account di servizio dedicato per la gestione dei pacchetti FRL. Se non disponi già di un account dedicato, puoi seguire [questo video di istruzioni](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) per scoprire come aggiungere un nuovo utente alla tua organizzazione Adobe.

Una volta che disponi dell’account appropriato, segui questi passaggi per concedere le autorizzazioni di download:

1. In Admin Console, passa alla scheda **Utenti**.
2. Individua o crea un account utente per concedere le autorizzazioni di download.
3. Fai clic sul nome dell’utente per aprire il suo profilo.
4. Fare clic sull&#39;icona accanto all&#39;utente **Modifica diritti amministratore**.
5. Assegna all&#39;utente il ruolo **Amministratore distribuzione**. Possono funzionare anche altri ruoli amministratore, ma il ruolo consigliato è Amministratore distribuzione. Fai clic su **Salva**.


##### Distribuire il pacchetto FRL (server AEM Forms)

I seguenti passaggi vengono eseguiti sul server AEM Forms, con i diritti di *amministratore locale* sul computer.

###### Passaggio 4: accedi al server che esegue AEM Forms come amministratore

Accedi al server che esegue AEM Forms utilizzando il metodo appropriato. Verificare di utilizzare un account con privilegi di amministratore locale per accedere al server.

###### Passaggio 5: disinstallare la versione precedente di Acrobat (se presente)

**Critico:** Prima di disinstallare, esegui il backup di impostazioni, profili o configurazioni Acrobat personalizzate.

1. Aprire il Pannello di controllo Campaign Windows.
2. Passa a **Impostazioni** e apri **App**.
3. Individua **Adobe Acrobat** nell&#39;elenco dei programmi installati
4. Seleziona **Disinstalla** e segui le istruzioni per rimuovere l&#39;applicazione. Se richiesto, riavviare il server
5. Verificare che tutte le versioni Classic del programma siano disinstallate. Se necessario, usa lo strumento [Adobe Acrobat Cleaner](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) per completare la rimozione.

###### Passaggio 6: Scaricare e installare Adobe Acrobat Pro

Dopo aver disinstallato la versione precedente, è necessario scaricare e installare una versione compatibile di Adobe Acrobat Pro:

1. Vai alla [pagina Download di Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Passa alla sezione **Programma di installazione di Acrobat Pro**.
3. Per l’utilizzo con AEM Forms PDF Generator, scarica il programma di installazione &quot;For Windows (32-Bit)&quot;, in quanto questa è la versione supportata con AEM Forms PDF Generator.
4. Seguire le istruzioni di installazione riportate nella pagina:
   * Estrai il file zip scaricato in una cartella sul computer
   * Passare al file Setup.exe (non eseguire il file Setup.exe dal file zip)
   * Fare doppio clic su Setup.exe per avviare l&#39;installazione
   * Seguire le istruzioni visualizzate sullo schermo per completare l&#39;installazione
5. Dopo l&#39;installazione, aprire Adobe Acrobat Pro e completare la configurazione iniziale eliminando le finestre di dialogo di benvenuto.
6. Verificare l&#39;installazione creando un PDF semplice.

###### Passaggio 7: scaricare il pacchetto FRL

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/) utilizzando l&#39;*account utente* a cui hai fornito le autorizzazioni di download al passaggio 3.
1. Passa alla scheda **Pacchetti**.
1. Individua il pacchetto FRL creato nel passaggio 2 (denominato &quot;Acrobat FRL AEM Forms&quot; o il nome del pacchetto personalizzato).
1. Fai clic su **Scarica** per scaricare il pacchetto sul server.

###### Passaggio 8: distribuire il pacchetto

1. **Estrarre il pacchetto:** Estrarre il contenuto del file ZIP scaricato in una directory sul server (ad esempio, `C:\AcrobatFRL`). Assicurati che la directory di estrazione sia facilmente accessibile.

2. **Apri prompt dei comandi come amministratore (Windows):** Fare clic con il pulsante destro del mouse sul pulsante Start e selezionare &quot;Prompt dei comandi (Admin)&quot; o &quot;Windows PowerShell (Admin)&quot;

3. **Accedere alla directory di estrazione:**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Esegui il comando di attivazione:**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Importante:**
   > * Sostituisci `<JSON_FILE_NAME>.json` con il nome file *exact* del file JSON nel pacchetto estratto.
   > * Il nome del file JSON distingue tra maiuscole e minuscole.
   > * Controllare il nome del file per eventuali errori di battitura.

   **Output previsto:**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **Nota:** Il processo di attivazione potrebbe richiedere circa 30 secondi.

5. **Informazioni sui parametri del comando:**

   | Parametro | Descrizione |
   |-----------|-------------|
   | `-p` | Specifica la piattaforma (rileva automaticamente il sistema operativo) |
   | `-i` | Indica allo strumento di installare e attivare la licenza |
   | `-f` | Specifica il percorso del file di licenza JSON |

###### Passaggio 9: avviare il server AEM Forms

Dopo aver completato tutti i processi, eseguire un test di azione rapida per confermare la validità dell&#39;installazione:

1. Avvia il server AEM Forms da una console della riga di comando all’interno di una sessione utente interattiva. (Accedi al server e avvia manualmente AEM Forms dalla riga di comando.)
2. Mantenere attiva la sessione utente dopo l&#39;avvio del server. Non uscire dal computer, poiché il processo server verrà interrotto. È possibile chiudere la finestra di Desktop remoto senza disconnettersi; il server continua a funzionare finché la sessione rimane attiva.
3. Per una maggiore affidabilità, configura un’attività di avvio o un’attività pianificata per avviare automaticamente il server AEM Forms al momento dell’accesso dell’utente.

###### Passaggio 10 Test del servizio PDF Generator

1. Aprire l’interfaccia di amministrazione di AEM Forms
2. Passare al servizio PDF Generator
3. Provare a convertire un semplice documento di Microsoft Office in PDF
4. Verifica che la conversione sia stata completata correttamente

#### Verifica della versione di Acrobat dopo l&#39;attivazione FRL

1. Apri Adobe Acrobat Pro DC sul server
2. Vai alla → Informazioni su Adobe Acrobat Pro DC
3. Verifica che il numero di versione corrisponda alla versione prevista
4. Conferma che lo stato della licenza sia attivato

>[!TAB Contratto multilicenza - Utente singolo]

#### Impostazione delle licenze FRL (Feature Restricted Licensing) per Adobe Acrobat sul server AEM Forms

Questi passaggi presuppongono che tu disponga dei privilegi di amministratore necessari sia sul Adobe Admin Console che sul server che esegue AEM Forms.

##### Preparare il pacchetto FRL (Adobe Admin Console)

Questi passaggi devono essere eseguiti con l&#39;accesso *Amministratore di sistema* a Adobe Admin Console.

###### Passaggio 1: accedere a Adobe Admin Console

1. Apri un browser Web e passa a [Adobe Admin Console](https://adminconsole.adobe.com/)
1. Accedi utilizzando un account con *privilegi di amministratore di sistema*.
1. (Facoltativo) Se la tua organizzazione ha accesso a più organizzazioni IMS, utilizza l’opzione di selezione dell’organizzazione nell’angolo in alto a destra di Admin Console per scegliere l’organizzazione corretta. Nella maggior parte degli scenari dei clienti, questo sarebbe già impostato sul valore predefinito della tua organizzazione, in quanto gli utenti in genere hanno accesso solo alla propria organizzazione.

###### Passaggio 2: creare il pacchetto FRL

1. In Admin Console, passa alla scheda &quot;Pacchetti&quot;. Questo è un pacchetto Adobe Admin Console, non un pacchetto AEM.
1. Selezionare la scheda **Feature Restricted License** e fare clic sul pulsante **Inizia**. Accertarsi di selezionare il tipo di licenza corretto.
1. Nella schermata **Crea pacchetto**, configurare le impostazioni del pacchetto:

   | Impostazione | Valore consigliato | Note |
   |---------|-------------------|-------|
   | Metodo di attivazione | Offline | Opzione consigliata |
   | Diritto | Generazione PDF (PDFG) | Richiesto per la funzionalità AEM Forms PDF Generator |
   | Configura piattaforma | Windows a 64 bit | Apple macOS non è attualmente supportato |
   | Abilita locale | &quot;Usa lingua del sistema operativo&quot; | Impostazione predefinita |
   | Lingua | Lingua preferita | Per l’interfaccia di Acrobat |
   | Scegli le app - applicazioni disponibili | Mantieni Adobe Acrobat nelle applicazioni disponibili. Non spostare nell&#39;applicazione selezionata | Puoi [scaricare Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) dalla pagina Adobe Experience League al passaggio 6. |
   | Scegli app - applicazioni selezionate | Mantieni solo file di licenza nelle applicazioni selezionate | Impostazione predefinita per la distribuzione FRL |
   | Plug-in | Non apportare modifiche in questa schermata | |
   | Opzioni | Non apportare modifiche in questa schermata | |
   | Finalizza | Nome pacchetto: &quot;Acrobat FRL AEM Forms&quot; | Utilizza un nome descrittivo |

1. Fai clic su **Crea** per creare il pacchetto.

###### Passaggio 3: fornire le autorizzazioni per il download a un utente

Si consiglia di creare un account di servizio dedicato per la gestione dei pacchetti FRL. Se non disponi già di un account dedicato, puoi seguire [questo video di istruzioni](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) per scoprire come aggiungere un nuovo utente alla tua organizzazione Adobe.

Una volta che disponi dell’account appropriato, segui questi passaggi per concedere le autorizzazioni di download:

1. In Admin Console, passa alla scheda **Utenti**.
2. Individua o crea un account utente per concedere le autorizzazioni di download.
3. Fai clic sul nome dell’utente per aprire il suo profilo.
4. Fare clic sull&#39;icona accanto all&#39;utente **Modifica diritti amministratore**.
5. Assegna all&#39;utente il ruolo **Amministratore distribuzione**. Possono funzionare anche altri ruoli amministratore, ma il ruolo consigliato è Amministratore distribuzione. Fai clic su **Salva**.


##### Distribuire il pacchetto FRL (server AEM Forms)

I seguenti passaggi vengono eseguiti sul server AEM Forms, con i diritti di *amministratore locale* sul computer.

###### Passaggio 4: accedi al server che esegue AEM Forms come amministratore

Accedi al server che esegue AEM Forms utilizzando il metodo appropriato. Verificare di utilizzare un account con privilegi di amministratore locale per accedere al server.

###### Passaggio 5: disinstallare la versione precedente di Acrobat (se presente)

**Critico:** Prima di disinstallare, esegui il backup di impostazioni, profili o configurazioni Acrobat personalizzate.

1. Aprire il Pannello di controllo Campaign Windows.
2. Passa a **Impostazioni** e apri **App**.
3. Individua **Adobe Acrobat** nell&#39;elenco dei programmi installati
4. Seleziona **Disinstalla** e segui le istruzioni per rimuovere l&#39;applicazione. Se richiesto, riavviare il server
5. Verificare che tutte le versioni Classic del programma siano disinstallate. Se necessario, usa lo strumento [Adobe Acrobat Cleaner](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) per completare la rimozione.

###### Passaggio 6: Scaricare e installare Adobe Acrobat Pro

Dopo aver disinstallato la versione precedente, è necessario scaricare e installare una versione compatibile di Adobe Acrobat Pro:

1. Vai alla [pagina Download di Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Passa alla sezione **Programma di installazione di Acrobat Pro**.
3. Per l’utilizzo con AEM Forms PDF Generator, scarica il programma di installazione &quot;For Windows (32-Bit)&quot;, in quanto questa è la versione supportata con AEM Forms PDF Generator.
4. Seguire le istruzioni di installazione riportate nella pagina:
   * Estrai il file zip scaricato in una cartella sul computer
   * Passare al file Setup.exe (non eseguire il file Setup.exe dal file zip)
   * Fare doppio clic su Setup.exe per avviare l&#39;installazione
   * Seguire le istruzioni visualizzate sullo schermo per completare l&#39;installazione
5. Dopo l&#39;installazione, aprire Adobe Acrobat Pro e completare la configurazione iniziale eliminando le finestre di dialogo di benvenuto.
6. Verificare l&#39;installazione creando un PDF semplice.

###### Passaggio 7: scaricare il pacchetto FRL

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/) utilizzando l&#39;*account utente* a cui hai fornito le autorizzazioni di download al passaggio 3.
1. Passa alla scheda **Pacchetti**.
1. Individua il pacchetto FRL creato nel passaggio 2 (denominato &quot;Acrobat FRL AEM Forms&quot; o il nome del pacchetto personalizzato).
1. Fai clic su **Scarica** per scaricare il pacchetto sul server.

###### Passaggio 8: distribuire il pacchetto

1. **Estrarre il pacchetto:** Estrarre il contenuto del file ZIP scaricato in una directory sul server (ad esempio, `C:\AcrobatFRL`). Assicurati che la directory di estrazione sia facilmente accessibile.

2. **Apri prompt dei comandi come amministratore (Windows):** Fare clic con il pulsante destro del mouse sul pulsante Start e selezionare &quot;Prompt dei comandi (Admin)&quot; o &quot;Windows PowerShell (Admin)&quot;

3. **Accedere alla directory di estrazione:**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Esegui il comando di attivazione:**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Importante:**
   > * Sostituisci `<JSON_FILE_NAME>.json` con il nome file *exact* del file JSON nel pacchetto estratto.
   > * Il nome del file JSON distingue tra maiuscole e minuscole.
   > * Controllare il nome del file per eventuali errori di battitura.

   **Output previsto:**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **Nota:** Il processo di attivazione potrebbe richiedere circa 30 secondi.

5. **Informazioni sui parametri del comando:**

   | Parametro | Descrizione |
   |-----------|-------------|
   | `-p` | Specifica la piattaforma (rileva automaticamente il sistema operativo) |
   | `-i` | Indica allo strumento di installare e attivare la licenza |
   | `-f` | Specifica il percorso del file di licenza JSON |

###### Passaggio 9: avviare il server AEM Forms

Dopo aver completato tutti i processi, eseguire un test di azione rapida per confermare la validità dell&#39;installazione:

1. Utilizzare Desktop remoto (RDP) per accedere al server e avviare il server AEM Forms utilizzando i servizi.
2. Utilizzare Desktop remoto (RDP) per accedere al server e avviare il server AEM Forms utilizzando Servizi Windows. Una volta che il server è in esecuzione, non chiudere semplicemente la finestra RDP. Disconnettersi dall&#39;utente per garantire che la sessione termini correttamente mentre il servizio continua a essere eseguito in background.

###### Passaggio 10: verifica del servizio PDF Generator

Dopo aver completato tutti i processi, eseguire un test di azione rapida per confermare la validità dell&#39;installazione:

1. Aprire l’interfaccia di amministrazione di AEM Forms
2. Passare al servizio PDF Generator
3. Provare a convertire un semplice documento di Microsoft Office in PDF
4. Verifica che la conversione sia stata completata correttamente

###### Passaggio 11: verificare la versione di Acrobat dopo l’attivazione della FRL

1. Apri Adobe Acrobat Pro DC sul server
2. Vai alla → Informazioni su Adobe Acrobat Pro DC
3. Verifica che il numero di versione corrisponda alla versione prevista
4. Conferma che lo stato della licenza sia attivato

>[!TAB Volume License - Più Utenti]

#### Impostazione delle licenze FRL (Feature Restricted Licensing) per Adobe Acrobat sul server AEM Forms

Questi passaggi presuppongono che tu disponga dei privilegi di amministratore necessari sia sul Adobe Admin Console che sul server che esegue AEM Forms.

##### Preparare il pacchetto FRL (Adobe Admin Console)

Questi passaggi devono essere eseguiti con l&#39;accesso *Amministratore di sistema* a Adobe Admin Console.

###### Passaggio 1: accedere a Adobe Admin Console

1. Apri un browser Web e passa a [Adobe Admin Console](https://adminconsole.adobe.com/)
1. Accedi utilizzando un account con *privilegi di amministratore di sistema*.
1. (Facoltativo) Se la tua organizzazione ha accesso a più organizzazioni IMS, utilizza l’opzione di selezione dell’organizzazione nell’angolo in alto a destra di Admin Console per scegliere l’organizzazione corretta. Nella maggior parte degli scenari dei clienti, questo sarebbe già impostato sul valore predefinito della tua organizzazione, in quanto gli utenti in genere hanno accesso solo alla propria organizzazione.

###### Passaggio 2: creare il pacchetto FRL

1. In Admin Console, passa alla scheda &quot;Pacchetti&quot;. Questo è un pacchetto Adobe Admin Console, non un pacchetto AEM.
1. Selezionare la scheda **Feature Restricted License** e fare clic sul pulsante **Inizia**. Accertarsi di selezionare il tipo di licenza corretto.
1. Nella schermata **Crea pacchetto**, configurare le impostazioni del pacchetto:

   | Impostazione | Valore consigliato | Note |
   |---------|-------------------|-------|
   | Metodo di attivazione | Offline | Opzione consigliata |
   | Diritto | Generazione PDF (PDFG) | Richiesto per la funzionalità AEM Forms PDF Generator |
   | Configura piattaforma | Windows a 64 bit | Apple macOS non è attualmente supportato |
   | Abilita locale | &quot;Usa lingua del sistema operativo&quot; | Impostazione predefinita |
   | Lingua | Lingua preferita | Per l’interfaccia di Acrobat |
   | Scegli le app - applicazioni disponibili | Mantieni Adobe Acrobat nelle applicazioni disponibili. Non spostare nell&#39;applicazione selezionata | Puoi [scaricare Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) dalla pagina Adobe Experience League al passaggio 6. |
   | Scegli app - applicazioni selezionate | Mantieni solo file di licenza nelle applicazioni selezionate | Impostazione predefinita per la distribuzione FRL |
   | Plug-in | Non apportare modifiche in questa schermata | |
   | Opzioni | Non apportare modifiche in questa schermata | |
   | Finalizza | Nome pacchetto: &quot;Acrobat FRL AEM Forms&quot; | Utilizza un nome descrittivo |

1. Fai clic su **Crea** per creare il pacchetto.

###### Passaggio 3: fornire le autorizzazioni per il download a un utente

Si consiglia di creare un account di servizio dedicato per la gestione dei pacchetti FRL. Se non disponi già di un account dedicato, puoi seguire [questo video di istruzioni](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) per scoprire come aggiungere un nuovo utente alla tua organizzazione Adobe.

Una volta che disponi dell’account appropriato, segui questi passaggi per concedere le autorizzazioni di download:

1. In Admin Console, passa alla scheda **Utenti**.
2. Individua o crea un account utente per concedere le autorizzazioni di download.
3. Fai clic sul nome dell’utente per aprire il suo profilo.
4. Fare clic sull&#39;icona accanto all&#39;utente **Modifica diritti amministratore**.
5. Assegna all&#39;utente il ruolo **Amministratore distribuzione**. Possono funzionare anche altri ruoli amministratore, ma il ruolo consigliato è Amministratore distribuzione. Fai clic su **Salva**.


##### Distribuire il pacchetto FRL (server AEM Forms)

I seguenti passaggi vengono eseguiti sul server AEM Forms, con i diritti di *amministratore locale* sul computer.

###### Passaggio 4: accedi al server che esegue AEM Forms come amministratore

Accedi al server che esegue AEM Forms utilizzando il metodo appropriato. Verificare di utilizzare un account con privilegi di amministratore locale per accedere al server.

###### Passaggio 5: disinstallare la versione precedente di Acrobat (se presente)

**Critico:** Prima di disinstallare, esegui il backup di impostazioni, profili o configurazioni Acrobat personalizzate.

1. Aprire il Pannello di controllo Campaign Windows.
2. Passa a **Impostazioni** e apri **App**.
3. Individua **Adobe Acrobat** nell&#39;elenco dei programmi installati
4. Seleziona **Disinstalla** e segui le istruzioni per rimuovere l&#39;applicazione. Se richiesto, riavviare il server
5. Verificare che tutte le versioni Classic del programma siano disinstallate. Se necessario, usa lo strumento [Adobe Acrobat Cleaner](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) per completare la rimozione.

###### Passaggio 6: Scaricare e installare Adobe Acrobat Pro

Dopo aver disinstallato la versione precedente, è necessario scaricare e installare una versione compatibile di Adobe Acrobat Pro:

1. Vai alla [pagina Download di Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Passa alla sezione **Programma di installazione di Acrobat Pro**.
3. Per l’utilizzo con AEM Forms PDF Generator, scarica il programma di installazione &quot;For Windows (32-Bit)&quot;, in quanto questa è la versione supportata con AEM Forms PDF Generator.
4. Seguire le istruzioni di installazione riportate nella pagina:
   * Estrai il file zip scaricato in una cartella sul computer
   * Passare al file Setup.exe (non eseguire il file Setup.exe dal file zip)
   * Fare doppio clic su Setup.exe per avviare l&#39;installazione
   * Seguire le istruzioni visualizzate sullo schermo per completare l&#39;installazione
5. Dopo l&#39;installazione, aprire Adobe Acrobat Pro e completare la configurazione iniziale eliminando le finestre di dialogo di benvenuto.
6. Verificare l&#39;installazione creando un PDF semplice.

###### Passaggio 7: scaricare il pacchetto FRL

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/) utilizzando l&#39;*account utente* a cui hai fornito le autorizzazioni di download al passaggio 3.
1. Passa alla scheda **Pacchetti**.
1. Individua il pacchetto FRL creato nel passaggio 2 (denominato &quot;Acrobat FRL AEM Forms&quot; o il nome del pacchetto personalizzato).
1. Fai clic su **Scarica** per scaricare il pacchetto sul server.

###### Passaggio 8: distribuire il pacchetto

1. **Estrarre il pacchetto:** Estrarre il contenuto del file ZIP scaricato in una directory sul server (ad esempio, `C:\AcrobatFRL`). Assicurati che la directory di estrazione sia facilmente accessibile.

2. **Apri prompt dei comandi come amministratore (Windows):** Fare clic con il pulsante destro del mouse sul pulsante Start e selezionare &quot;Prompt dei comandi (Admin)&quot; o &quot;Windows PowerShell (Admin)&quot;

3. **Accedere alla directory di estrazione:**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Esegui il comando di attivazione:**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Importante:**
   > * Sostituisci `<JSON_FILE_NAME>.json` con il nome file *exact* del file JSON nel pacchetto estratto.
   > * Il nome del file JSON distingue tra maiuscole e minuscole.
   > * Controllare il nome del file per eventuali errori di battitura.

   **Output previsto:**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **Nota:** Il processo di attivazione potrebbe richiedere circa 30 secondi.

5. **Informazioni sui parametri del comando:**

   | Parametro | Descrizione |
   |-----------|-------------|
   | `-p` | Specifica la piattaforma (rileva automaticamente il sistema operativo) |
   | `-i` | Indica allo strumento di installare e attivare la licenza |
   | `-f` | Specifica il percorso del file di licenza JSON |

###### Passaggio 9: avviare il server AEM Forms

Dopo aver completato tutti i processi, eseguire un test di azione rapida per confermare la validità dell&#39;installazione:

1. Avvia il server AEM Forms da una console della riga di comando all’interno di una sessione utente interattiva. (Accedi al server e avvia manualmente AEM Forms dalla riga di comando.)
2. Mantenere attiva la sessione utente dopo l&#39;avvio del server. Non uscire dal computer, poiché il processo server verrà interrotto. È possibile chiudere la finestra di Desktop remoto senza disconnettersi; il server continua a funzionare finché la sessione rimane attiva.
3. Per una maggiore affidabilità, configura un’attività di avvio o un’attività pianificata per avviare automaticamente il server AEM Forms al momento dell’accesso dell’utente.

###### Passaggio 10: verifica del servizio PDF Generator

Dopo aver completato tutti i processi, eseguire un test di azione rapida per confermare la validità dell&#39;installazione:

1. Aprire l’interfaccia di amministrazione di AEM Forms
2. Passare al servizio PDF Generator
3. Provare a convertire un semplice documento di Microsoft Office in PDF
4. Verifica che la conversione sia stata completata correttamente

#### Verifica della versione di Acrobat dopo l&#39;attivazione FRL

1. Apri Adobe Acrobat Pro DC sul server
2. Vai alla → Informazioni su Adobe Acrobat Pro DC
3. Verifica che il numero di versione corrisponda alla versione prevista
4. Conferma che lo stato della licenza sia attivato

>[!ENDTABS]



### Disabilita modalità protetta all’avvio in Acrobat

Dopo aver abilitato Feature Restricted Licensing (FRL) e verificato l’attivazione di Acrobat, si consiglia di disabilitare la modalità protetta all’avvio in Adobe Acrobat per garantire la compatibilità con AEM Forms PDF Generator.

Segui questi passaggi:

1. Aprire **Adobe Acrobat Pro DC** sul server.
2. Vai a **Menu** > **Preferenze**.
3. Nella finestra Preferenze, seleziona **Protezione (avanzata)** dal riquadro a sinistra.
4. Nella sezione **Sandbox Protections**, **deseleziona** l&#39;opzione **&quot;Enable Protected Mode at startup&quot;**.
5. Fare clic su **Sì** se viene richiesta la conferma.
6. Fai clic su **OK** per salvare le modifiche e chiudere la finestra Preferenze.
7. Riavviare Adobe Acrobat Pro DC per rendere effettive le modifiche.

>[!NOTE]
>
>La disattivazione della modalità protetta è necessaria per scenari di automazione lato server come AEM Forms PDF Generator. Questa impostazione deve essere modificata solo in ambienti server dedicati e non nei desktop degli utenti finali.

Per ulteriori informazioni, consulta la [documentazione di Adobe sulla modalità protetta](https://helpx.adobe.com/acrobat/kb/protected-mode-troubleshooting-reader.html).



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
   <td><p>C:\Program Files\Java\jdk11</p> </td>
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
>     * Assicurati che la variabile `OpenOffice_PATH` sia impostata a livello globale (ad esempio, utilizzando `/etc/profile` o l&#39;equivalente specifico del sistema) in modo che sia disponibile per tutti gli utenti al momento dell&#39;accesso.

### (Solo per IBM® WebSphere®) Configurazione del provider del socket SSL IBM® {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

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
1. Nell&#39;elenco **[!UICONTROL Tipo file]** deselezionare **[!UICONTROL Apri]** per il tipo di file che il servizio PDF Generator deve essere in grado di convertire in documenti PDF.

### (Solo Windows) Concedere il privilegio del token di livello processo Sostituisci {#grant-the-replace-a-process-level-token-privilege}

L&#39;account utente utilizzato per avviare il server applicazioni richiede il privilegio **Replace a process level token**. L&#39;account di sistema locale dispone del privilegio **Sostituisci un token a livello di processo** per impostazione predefinita. Per i server in esecuzione con un utente del gruppo Administrators locale, è necessario concedere esplicitamente il privilegio. Per concedere il privilegio, effettua le seguenti operazioni:

1. Aprire Editor Criteri di gruppo per Microsoft® Windows. Per aprire l&#39;Editor Criteri di gruppo, fare clic su **[!UICONTROL Inizio]**, digitare **gpedit.msc** nella casella Avvia ricerca, quindi fare clic su **[!UICONTROL Editor Criteri di gruppo]**.
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

Durante la conversione di un documento in PDF tramite il servizio PDF Generator su Windows Server, in alcuni casi Windows Server segnala che l&#39;eseguibile ha riscontrato un problema e deve essere chiuso. Tuttavia, non influisce sulla conversione PDF in quanto continua in background.

Per evitare di ricevere l&#39;errore, è possibile disattivare la segnalazione errori di Windows. Per ulteriori informazioni sulla disattivazione della segnalazione errori, vedere [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

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
1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu intestazione.
1. Nella sezione **[!UICONTROL Filtri]**:
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
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

1. Nella scheda **[!UICONTROL Account utente]**, fornisci le credenziali di un account utente locale e fai clic su **[!UICONTROL Invia]**. Se Microsoft® Windows richiede, consenti l’accesso all’utente. Una volta aggiunto, l&#39;utente configurato viene visualizzato nella sezione **[!UICONTROL Account utente]** della scheda **[!UICONTROL Account utente]**.

### Configurare le impostazioni di timeout {#configure-the-time-out-settings}

1. In [Gestione configurazione AEM](http://localhost:4502/system/console/configMgr), individuare e aprire il servizio **[!UICONTROL Provider ORB Jacorb]**.

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
   <td>Numero di secondi necessari per eseguire operazioni post-conversione.<br /> </td>
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
   1. Passa a `[extracted-zip-file]\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\`
   1. Decomprimi `adobe-aemfd-pdfg-common-pkg-[version]`.
   1. Passare alla directory `[downloaded-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]`. Esegui il seguente file batch:

      `Acrobat_for_PDFG_Configuration.bat`

      Acrobat è configurato per l’esecuzione con il servizio PDF Generator.

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
1. Fai clic sul campo **[!UICONTROL name]** dell&#39;account utente. Viene visualizzata la pagina **[!UICONTROL Modifica impostazioni utente]**. Nell’istanza Autore AEM, i certificati risiedono in un KeyStore. Se in precedenza non è stato creato un KeyStore, fare clic su **[!UICONTROL Crea KeyStore]** e impostare una nuova password per il KeyStore. Se il server contiene già un KeyStore, salta questo passaggio.  Se utilizzi il certificato Reader Extensions di Adobe, la password del file Keystore è sempre la stessa della password della chiave privata.
1. Nella pagina **[!UICONTROL Modifica impostazioni utente]** selezionare la scheda **[!UICONTROL KeyStore]**. Espandere l&#39;opzione **[!UICONTROL Aggiungi chiave privata dal file dell&#39;archivio chiavi]** e specificare un alias. L’alias viene utilizzato per eseguire l’operazione Reader Extensions.
1. Per caricare il file del certificato, fare clic su **[!UICONTROL Seleziona file di archivio chiavi]** e caricare un file &lt;nomefile>.pfx.

   Aggiungi **[!UICONTROL Password archivio chiavi]**, **[!UICONTROL Password chiave privata]** e **[!UICONTROL Alias chiave privata]** associati al certificato ai rispettivi campi. Fai clic su **[!UICONTROL Invia]**.

   >[!NOTE]
   >
   >Nell’ambiente di produzione, sostituisci le credenziali di valutazione con le credenziali di produzione. Prima di aggiornare una credenziale scaduta o di valutazione, accertati di eliminare le vecchie credenziali delle estensioni Reader.

1. Fare clic su **[!UICONTROL Salva e chiudi]** nella pagina **[!UICONTROL Modifica impostazioni utente]**.

### Abilita AES-256 {#enable-aes}

Per utilizzare la crittografia AES 256 per i file PDF, è necessario ottenere e installare i file Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy. Sostituisci i file local_policy.jar e US_export_policy.jar nella cartella jre/lib/security. Ad esempio, se si utilizza Sun JDK, copiare i file scaricati nella cartella `[JAVA_HOME]/jre/lib/security`.

Il servizio Assembler dipende dal servizio Reader Extensions, dal servizio Signature, dal servizio Forms e dal servizio Output. Per verificare che i servizi richiesti siano operativi, effettua le seguenti operazioni:

1. Accedere all&#39;URL `https://'[server]:[port]'/system/console/bundles` come amministratore.
1. Cerca nel seguente servizio e assicurati che i servizi siano attivi e funzionanti:

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

## Risoluzione di problemi

Se si verificano problemi anche dopo aver risolto tutti i problemi segnalati dallo strumento SRT, eseguire i controlli seguenti:

Prima di eseguire i controlli seguenti, verificare che [Strumento di preparazione al sistema](#SRT) non riporti alcun errore.

+++ Adobe Acrobat

* Verificare che sia installata solo la [versione supportata](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) di Microsoft® Office (32 bit) e Adobe Acrobat e che le finestre di dialogo di apertura siano annullate.
<!-- (Acrobat 2020 only) Ensure that Adobe Acrobat Update Service is disabled. -->
* Verificare che il file batch [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) sia stato eseguito con privilegi di amministratore.
* Accertati che un utente PDF Generator sia aggiunto nell’interfaccia utente di configurazione di PDF.
* Assicurarsi che sia stata aggiunta l&#39;autorizzazione [Sostituisci un token a livello di processo](#grant-the-replace-a-process-level-token-privilege) per l&#39;utente PDF Generator.
* Verificare che Acrobat PDFMaker Office COM Addin sia abilitato per le applicazioni Microsoft Office.

+++

+++OpenOffice

**Microsoft® Windows**

* Verificare che sia installata la versione [supportata](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) di Microsoft Office a 32 bit e che le finestre di dialogo di apertura vengano annullate per tutte le applicazioni.
* Accertati che un utente PDF Generator sia aggiunto nell’interfaccia utente di configurazione di PDF.
* Verificare che l&#39;utente PDF Generator sia membro del gruppo Administrators e che il privilegio [Sostituisci token a livello di processo](#grant-the-replace-a-process-level-token-privilege) sia impostato per l&#39;utente.
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

<!-- +++ Unable to add a PDF Generator (PDFG) user

* (Acrobat 2020 only) Ensure Microsoft&reg; Visual C++ 2012 x86 and Microsoft&reg; Visual C++ 2013 x86 (32-bit) redistributable are installed on Windows.

+++
-->
+++Errori di test di automazione

* Per Microsoft® Office e OpenOffice, eseguire almeno una conversione manualmente (come ogni utente) per assicurarsi che non venga visualizzata alcuna finestra di dialogo durante la conversione. Se viene visualizzata una finestra di dialogo, chiuderla. Durante la conversione automatica non dovrebbe essere visualizzata alcuna finestra di dialogo di questo tipo.

* Prima di eseguire l’automazione in un ambiente AEM Forms su OSGi, assicurati che il pacchetto di test sia installato e attivo.

+++

<!-- +++ (Acrobat 2020 only) Multiple user conversion failures 

* Verify the server logs to check if the conversion is failing for a particular user.(Process Explorer can help you check running process for different users)

* Ensure that the user configured for PDF Generator has local admin rights.

* Ensure that PDF Generator user has read, write, and execute permissions on LC temp and PDFG temp users.

* For Microsoft&reg; Office and OpenOffice, perform at least one conversion manually (as each user) to ensure that no dialogue pops up during conversion. If any dialogue appears, dismissed it. No such dialogue should appear during automated conversion.

* Perform a sample conversion.

+++ -->

<!-- (Acrobat 2020 only) License of Adobe Acrobat installed on AEM Forms Server expires

* If you have an existing license of Adobe Acrobat and it has expired, [Download the latest version of Adobe Application Manager](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html), and migrating your serial number. Before [migrating your serial number](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * Use the following commands to generate prov.xml and reserialize the existing install using the prov.xml file instead of commands provided in [migrating your serial number](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) number article.

      ```

         adobe_prtk --tool=VolumeSerialize --generate --serial=<serialnum> [--leid=<LEID>] [--regsuppress=ss] [--eulasuppress] [--locales=limited list of locales in xx_XX format or ALL>] [--provfile=<Absolute path to prov.xml>]

      ```

   * Volume serialize the package (Re-serialize the existing install using the prov.xml file and the new serial): Run the following command from the PRTK installation folder as an administrator to serialize and activate the deployed packages on client machines:

      ```
         adobe_prtk --tool=VolumeSerialize --provfile=C:\prov.xml –stream
         
      ```

* For large-scale installations, use the [Acrobat Customization Wizard](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) to remove previous versions of Reader and Acrobat. Customize the installer and deploy it to all the machines of your organization.

(Acrobat 2020 only) AEM Forms Server is in an offline or secure environment and internet is not available to activate Acrobat.

* You can go online within 7 days of the first launch of your Adobe product to complete an online activation and registration or use an internet-enabled device and your product's serial number to complete this process. For detailed instructions, see [Offline Activation](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++ -->

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
