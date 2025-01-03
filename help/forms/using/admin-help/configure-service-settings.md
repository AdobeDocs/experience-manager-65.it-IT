---
title: Configurare le impostazioni del servizio
description: Scopri come configurare le impostazioni del servizio. È possibile utilizzare la pagina Gestione dei servizi per configurare le impostazioni per ciascuno dei servizi che fanno parte dei moduli AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: a6a10ff0-6f4d-42df-9b4e-f98a53cf1806
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Workbench
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '10836'
ht-degree: 0%

---

# Configurare le impostazioni del servizio {#configure-service-settings}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

È possibile utilizzare la pagina Gestione dei servizi per configurare le impostazioni per ciascuno dei servizi che fanno parte dei moduli AEM. Le impostazioni disponibili variano a seconda del servizio configurato.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Arrestare il servizio prima di modificarlo. (Vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
1. Fare clic sul nome del servizio che si desidera configurare.
1. Se il servizio dispone di una scheda Configurazione, utilizzarla per modificare le impostazioni del servizio. Per ulteriori informazioni, consulta l’elenco dei collegamenti riportati di seguito.

   >[!NOTE]
   >
   >Non tutti i servizi elencati nella pagina Gestione dei servizi dispongono di una scheda Configurazione. Per i processi creati, la scheda Configurazione viene visualizzata solo se è stato aggiunto un parametro di configurazione al processo in Workbench. (Vedi &quot;Parametri di configurazione&quot; nella [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) .)


1. Fare clic sulla scheda Protezione e impostare le impostazioni di protezione per il servizio. Vedere [Modifica delle impostazioni di protezione per un servizio](configure-service-settings.md#modifying-security-settings-for-a-service).
1. Se il servizio dispone di una scheda Endpoints, utilizzarla per modificare le impostazioni dell&#39;endpoint. Vedi [Gestione degli endpoint](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md).
1. Fare clic sulla scheda Pooling e impostare le impostazioni di pooling. Vedere [Configurazione del pooling per un servizio](configure-service-settings.md#configuring-pooling-for-a-service).
1. Fai clic su Salva per salvare le modifiche o su Annulla per eliminarle.
1. Selezionare la casella di controllo accanto al nome del servizio e fare clic su Avvia per riavviare il servizio.

## Impostazioni del servizio Flusso di lavoro di controllo {#audit-workflow-service-settings}

Workbench consente di registrare le istanze del processo durante l’esecuzione e quindi riprodurle per osservare il comportamento del processo. (Vedere [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).) Per risparmiare spazio sul file system di Forms Server, è possibile limitare la quantità di dati di registrazione del processo archiviati. È possibile configurare le seguenti proprietà del servizio Servizio flusso di lavoro di controllo ( `AuditWorkflowService`):

**maxNumberOfRecordingInstances:** Numero massimo di registrazioni archiviate. Quando viene memorizzato il numero massimo, la registrazione meno recente viene rimossa dal file system quando viene creata una nuova registrazione. Questa proprietà è utile se si tende a creare molte registrazioni e si desidera rimuovere automaticamente le registrazioni precedenti. Il valore predefinito è 50.

**MaxNumberOfRecordingEntries:** il numero massimo di voci di dati che è possibile archiviare per ogni registrazione. Le immissioni di dati sono informazioni sulle operazioni del processo. Per ogni esecuzione di un&#39;operazione vengono memorizzate diverse voci, ad esempio se l&#39;operazione è stata avviata, se l&#39;operazione è stata completata e se il ciclo di lavorazione che porta all&#39;operazione è stato completato. Questa proprietà è utile quando i processi possono includere molte esecuzioni di operazioni, ad esempio quando si verifica un ciclo infinito. Il valore predefinito è 50.

## impostazioni del servizio forms con codice a barre {#barcoded-forms-service-settings}

Il servizio Forms con codice a barre `(BarcodedFormsService)` estrae i dati del codice a barre dalle immagini digitalizzate. Il servizio accetta come input un formato di codice a barre (TIFF o PDF) ed estrae la rappresentazione automatica dei dati codificati dal codice a barre.

Per il servizio Forms con codice a barre sono disponibili le seguenti impostazioni.

**Lettura a sinistra:** Se selezionata, le immagini del codice a barre vengono digitalizzate orizzontalmente da destra a sinistra.

**Lettura a destra:** Se selezionata, le immagini del codice a barre vengono digitalizzate orizzontalmente da sinistra a destra.

**Lettura:** Se selezionata, le immagini dei codici a barre vengono digitalizzate verticalmente dal basso verso l&#39;alto.

**Lettura in basso:** Se selezionata, le immagini dei codici a barre vengono digitalizzate verticalmente dall&#39;alto verso il basso.

>[!NOTE]
>
>Per impostazione predefinita, vengono selezionate tutte le opzioni. Deselezionare un&#39;opzione solo se si è certi che i codici a barre non verranno visualizzati in questo modo nei moduli.

**Percorso file di base:** Il percorso del file relativo ai parametri dei file di input e output batch per le operazioni Esegui processo file XML ed Esegui processo file flat viene risolto. Nelle configurazioni cluster, il percorso del file di base deve essere una posizione del file system condiviso alla quale tutti i nodi del cluster hanno accesso in lettura/scrittura.

**Nome Source dati:** il nome dell&#39;origine dati utilizzata per gestire le informazioni sullo stato e sulla cronologia dei processi di elaborazione batch. L&#39;origine dati specificata deve supportare le transazioni globali (XA).

## Impostazioni del servizio Central Migration Bridge (obsoleto) {#central-migration-bridge-service-settings}

Il servizio Central Migration Bridge ( `CentralMigrationBridge`) richiama un sottoinsieme di funzionalità Adobe Central Pro Output Server (Central), che include i comandi JFMERGE, JFTRANS e XMLIMPORT. Le operazioni del servizio Central Migration Bridge consentono di riutilizzare le seguenti risorse centrali nei moduli AEM:

* progettazione modello (&amp;ast;.ifd)
* modelli di output (&amp;ast;.mdf)
* file di dati (&amp;ast;.dat files)
* file preambolo (&amp;ast;.pre files)
* file di definizione dati (&amp;ast;.tdf)

Per il servizio Central Migration Bridge è disponibile l’impostazione seguente.

**Directory di installazione centrale:** La directory in cui è installato Adobe Central 5.7.

## Content Repository Connector per le impostazioni dei servizi EMC Documentum {#content-repository-connector-for-emc-documentum-service-settings}

Il servizio Content Repository Connector per EMC Documentum ( `EMCDocumentumContentRepositoryConnector`) consente di creare processi che interagiscono con i contenuti archiviati in un repository Documentum.

Per il servizio Content Repository Connector for EMC Documentum è disponibile la seguente impostazione.

**Percorso predefinito oggetto Asset Link:** La porzione predefinita del percorso nel repository Documentum per l&#39;archiviazione dell&#39;oggetto Asset Link. Il percorso effettivo è costituito dal percorso predefinito e dalla posizione del modello di modulo nel repository dei moduli AEM.

Ad esempio, se il percorso predefinito è impostato su `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects` e il modello di modulo è archiviato in una cartella `/Docbase/forms/`, l&#39;oggetto Asset Link viene archiviato nel percorso seguente:

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

Il valore predefinito di questa impostazione è `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## Connettore dell&#39;archivio dei contenuti per le impostazioni del servizio IBM FileNet {#content-repository-connector-for-ibm-filenet-service-settings}

Il connettore del repository dei contenuti per IBM FileNet consente di creare processi che interagiscono con il contenuto memorizzato in un repository IBM FileNet.

L&#39;impostazione seguente è disponibile per il connettore del repository dei contenuti per il servizio IBM FileNet.

**Percorso predefinito oggetto Asset Link:** La parte predefinita del percorso nell&#39;archivio IBM FileNet per l&#39;archiviazione dell&#39;oggetto Asset Link. Il percorso effettivo è costituito dal percorso predefinito e dalla posizione del modello di modulo nel repository dei moduli AEM.

Ad esempio, se il percorso predefinito è impostato su `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects` e il modello di modulo è archiviato in una cartella `/Docbase/forms/`, l&#39;oggetto Asset Link viene archiviato nel percorso seguente:

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

Il valore predefinito di questa impostazione è `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## Converti impostazioni servizio PDF {#convert-pdf-service-settings}

Il servizio Convert PDF ( `ConvertPdfService`) converte i documenti PDF in PostScript e in diversi formati immagine (JPEG, JPEG 2000, PNG e TIFF). La conversione di un documento PDF in PostScript è utile per la stampa automatica basata su server su qualsiasi stampante PostScript. La conversione di un documento PDF in un file TIFF multipagina è pratica quando si archiviano documenti in sistemi di gestione dei contenuti che non supportano i documenti PDF.

Per il servizio Convert PDF sono disponibili le impostazioni seguenti.

**Tipo di transazione:** Specifica la modalità di propagazione di un contesto di transazione a un&#39;operazione.

**Obbligatorio:** supporta un contesto di transazione se ne esiste uno; in caso contrario, viene creato un nuovo contesto di transazione. Questo è il valore predefinito.

**Richiede nuovo:** crea sempre un nuovo contesto di transazione. Se esiste un contesto di transazione attivo, viene sospeso.

**Timeout transazione (in sec):** il numero di secondi di attesa del provider di transazioni sottostante prima del rollback di una transazione che esegue il wrapping di questa operazione. Questo valore verrà ignorato se viene propagato un contesto di transazione esistente. Il valore predefinito è 180.

**Risoluzione di soglia per l&#39;arrotondamento (in dpi):** la risoluzione dell&#39;immagine al di sotto della quale l&#39;arrotondamento (o l&#39;antialiasing) viene applicato al testo, al tratto e alle immagini, se sono state selezionate le opzioni &quot;Applica arrotondamento a&quot; per tali elementi.

**Applica uniformità al testo:** Controlla l&#39;antialiasing del testo. Per disattivare l&#39;arrotondamento del testo e rendere il testo più nitido e più semplice da leggere con una lente di ingrandimento dello schermo, deselezionare questa casella di controllo.

**Applica uniformità a LineArt:** Applica l&#39;uniformità per rimuovere angoli bruschi nelle linee.

**Applica uniformità alle immagini:** Applica l&#39;uniformità per ridurre al minimo le modifiche improvvise nelle immagini.

## Impostazioni del servizio Distiller {#distiller-service-settings}

Il servizio Distiller ( `DistillerService`) converte i file PostScript, PostScript incapsulato (EPS) e PRN in file PDF in una rete.

Per il servizio Distiller sono disponibili le impostazioni seguenti.

**Impostazioni Adobe PDF:** Le seguenti impostazioni preconfigurate vengono applicate al PDF generato:

* Stampa di alta qualità
* Pagine di dimensioni eccessive
* PDFA1b 2005 CMYK
* PDFA1b 2005 RGB
* PDFX1a 2001
* PDFX3 2002
* Qualità della stampa
* Dimensione file minima
* Standard

È possibile creare nuove impostazioni tramite l’interfaccia utente di PDF Generator.

**Impostazioni protezione:** Impostazioni di protezione preconfigurate applicate ai documenti PDF generati. Il valore predefinito è No Security. Creare le impostazioni di protezione utilizzando PDF Generator, quindi immettere le impostazioni qui.

**Dimensione pool:** La dimensione iniziale del pool. Quando il servizio Distiller viene distribuito, questo numero viene utilizzato per determinare il numero di istanze di implementazione del servizio create e allocate al pool libero in attesa di richieste di chiamata. Il contenitore del servizio può quindi rispondere immediatamente alle richieste di chiamata senza dover prima inizializzare un&#39;istanza del servizio.

## Impostazioni del servizio Document Management {#document-management-service-settings}

>[!NOTE]
>
>Adobe LiveCycle® ® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulla persona. Il supporto di Content Services (obsoleto) termina il 12/31/2014. Adobe Consulta il [documento sul ciclo di vita del prodotto](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

Il servizio Document Management ( `DocumentManagementService`) consente ai processi di utilizzare la funzionalità di gestione dei contenuti fornita da Content Services (obsoleto). Le operazioni di gestione dei documenti forniscono le attività di base necessarie per mantenere spazi e contenuti nel sistema di gestione dei contenuti. Esempi di tali attività sono la copia, l&#39;eliminazione, lo spostamento, il recupero e l&#39;archiviazione del contenuto, la creazione di spazi e associazioni e l&#39;ottenimento e l&#39;impostazione degli attributi del contenuto.

Per il servizio Document Management sono disponibili le impostazioni seguenti.

**Schema archivio:** Schema dell&#39;archivio in cui si trova il contenuto. Il valore predefinito è workspace.

**Porta HTTP:** Porta utilizzata per accedere a Content Services (obsoleta). Il valore predefinito è 8080.

## Impostazioni del servizio e-mail {#email-service-settings}

L’e-mail viene comunemente utilizzata per distribuire contenuti o fornire informazioni sullo stato come parte di un processo automatizzato. Il servizio di posta elettronica ( `EmailService`) consente ai processi di ricevere messaggi di posta elettronica da un server POP3 o IMAP e di inviare messaggi di posta elettronica a un server SMTP.

Ad esempio, un processo utilizza il servizio E-mail per inviare un messaggio e-mail con un allegato del modulo PDF. Il servizio e-mail si connette a un server SMTP per inviare il messaggio e-mail con l’allegato. Il modulo PDF è progettato per consentire al destinatario di fare clic su Invia dopo aver completato il modulo. L’azione fa sì che il modulo venga restituito come allegato al server e-mail designato. Il servizio e-mail recupera il messaggio e-mail restituito e memorizza il modulo completato in una variabile del modulo dati del processo.

Per il servizio e-mail sono disponibili le seguenti impostazioni.

**Host SMTP:** l&#39;indirizzo IP o l&#39;URL del server SMTP da utilizzare per l&#39;invio di e-mail.

**Numero porta SMTP:** Porta utilizzata per la connessione al server SMTP.

**Autenticazione SMTP:** Selezionare se per connettersi al server SMTP è necessaria l&#39;autenticazione utente.

**Utente SMTP:** il nome utente dell&#39;account utente da utilizzare per accedere al server SMTP.

**Password SMTP:** la password associata all&#39;account utente SMTP.

**Protezione trasporto SMTP:** Protocollo di protezione da utilizzare per la connessione al server SMTP:

* Seleziona Nessuno se non viene utilizzato alcun protocollo (i dati vengono inviati in formato testo non crittografato)
* Selezionare SSL se si utilizza il protocollo Secure Sockets Layer.
* Seleziona TLS se viene utilizzato Transport Layer Security.

**Host POP3/IMAP:** l&#39;indirizzo IP o l&#39;URL del server POP3 o IMAP da utilizzare per l&#39;invio di messaggi di posta elettronica.

**Nome utente POP3/IMAP:** Il nome utente dell&#39;account utente da utilizzare per accedere al server POP3 o IMAP.

**Password POP3/IMAP:** la password associata all&#39;account utente POP3 o IMAP.

**Numero porta POP3/IMAP:** Porta utilizzata per la connessione al server POP3 o IMAP.

**POP3/IMAP:** Protocollo da utilizzare per l&#39;invio e la ricezione di posta elettronica.

**Ricezione protezione trasporto:** Protocollo di protezione da utilizzare per la connessione al server SMTP:

* Seleziona Nessuno se non viene utilizzato alcun protocollo (i dati vengono inviati in formato testo non crittografato).
* Selezionare SSL se si utilizza il protocollo Secure Sockets Layer.
* Seleziona TLS se viene utilizzato Transport Layer Security.

## Impostazioni del servizio di crittografia {#encryption-service-settings}

Il servizio di crittografia ( `EncryptionService`) consente di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l’accesso al contenuto. Se un documento PDF è crittografato con una password, l’utente deve specificare la password di apertura prima che il documento possa essere visualizzato in Adobe Reader o Adobe Acrobat. Analogamente, se un documento PDF è crittografato con un certificato, l’utente deve decrittografare il documento PDF con la chiave pubblica corrispondente al certificato (chiave privata) utilizzato per crittografare il documento PDF.

Per il servizio Crittografia sono disponibili le impostazioni seguenti.

**Server LDAP predefinito a cui connettersi:** Nome host del server LDAP utilizzato per recuperare i certificati per la crittografia dei documenti.

**Porta LDAP predefinita a cui connettersi:** Numero di porta del server LDAP.

**Nome utente LDAP predefinito:** Se il server LDAP richiede l&#39;autenticazione, specificare il nome utente da utilizzare per la connessione al server LDAP.

**Password LDAP predefinita:** Se il server LDAP richiede l&#39;autenticazione, specificare la password corrispondente al nome utente da utilizzare per connettersi al server LDAP.

>[!NOTE]
>
>Utilizza l’autenticazione semplice (nome utente e password) solo quando la connessione è protetta tramite SSL (utilizzando LDAPS).

<!-- **Compatibility Mode:**-->

## Impostazioni del servizio FTP {#ftp-service-settings}

Il servizio FTP ( `FTP`) consente ai processi di interagire con un server FTP. Le operazioni del servizio FTP possono recuperare file dal server FTP, inserirli nel server FTP ed eliminarli dal server FTP. Ad esempio, documenti come i report generati da un processo possono essere memorizzati su un server FTP per la distribuzione. In alternativa, un sistema esterno può generare alcuni file in base ai passaggi precedenti di un processo. In un passaggio successivo del processo, i file possono essere trasferiti in una posizione remota.

Per il servizio FTP sono disponibili le seguenti impostazioni.

**Host predefinito:** l&#39;indirizzo IP o l&#39;URL del server FTP.

**Porta predefinita:** Porta utilizzata per la connessione al server FTP. Il valore predefinito è 21.

**Nome utente predefinito:** Nome dell&#39;account utente che è possibile utilizzare per accedere al server FTP. L&#39;account utente deve disporre di privilegi sufficienti per eseguire le operazioni FTP richieste dal servizio.

**Password predefinita:** password da utilizzare con il nome utente specificato per l&#39;autenticazione con il server FTP.

## Genera impostazioni servizio PDF {#generate-pdf-service-settings}

Il servizio Generate PDF ( `GeneratePDFService`) converte i file in vari formati nativi in documenti PDF e converte i documenti PDF in diversi formati di file.

Per il servizio Generate PDF sono disponibili le impostazioni seguenti.

**Impostazioni Adobe PDF:** il nome delle impostazioni Adobe PDF preconfigurate da applicare a un processo di conversione, se tali impostazioni non sono specificate come parte dei parametri di chiamata API. Le impostazioni di Adobe PDF vengono configurate nella console di amministrazione facendo clic su Servizi > PDF Generator > Impostazioni Adobe PDF. Queste impostazioni sono applicabili solo alle conversioni basate su PDFMaker.

**Impostazioni protezione:** il nome delle impostazioni di protezione preconfigurate da applicare a un processo di conversione, se tali impostazioni non sono specificate come parte dei parametri di chiamata API. Le impostazioni di protezione vengono configurate nella console di amministrazione facendo clic su Servizi > PDF Generator > Impostazioni protezione.

**Impostazioni del tipo di file:** Il nome dell&#39;impostazione del tipo di file preconfigurato da applicare a un processo di conversione, se tali impostazioni non sono specificate come parte dei parametri di chiamata API. Le impostazioni del tipo di file vengono configurate nella console di amministrazione facendo clic su Servizi > PDF Generator > Impostazioni tipo di file.

**Usa WebCapture (solo Windows):** Quando questa impostazione è true, il servizio Generate PDF utilizza Acrobat per tutte le conversioni da HTML a PDF. Questo può migliorare la qualità dei file PDF prodotti da HTML, anche se le prestazioni possono essere leggermente inferiori. Il valore predefinito è false.

**Convertitore primario per le conversioni da HTML a PDF:** Il servizio Generate PDF fornisce più percorsi per la conversione di file HTML in documenti PDF: Webkit, WebCapture (solo Windows) e WebToPDF. Questa impostazione consente all&#39;utente di selezionare il convertitore primario per la conversione da HTML a PDF. Per impostazione predefinita, WebToPDF è selezionato.

**Convertitore di fallback per conversioni da HTML a PDF:** Se il convertitore primario non riesce, specificare il convertitore per conversioni da HTML a PDF. Per impostazione predefinita, WebCapture (solo Windows) è selezionato.

**Usa conversione immagine Acrobat (solo Windows):** Quando questa impostazione è True, il servizio Genera PDF utilizza Acrobat per tutte le conversioni da immagine a PDF. Questa impostazione è utile solo se il meccanismo di conversione Java puro predefinito non è in grado di convertire correttamente una proporzione significativa delle immagini di input. Il valore predefinito è false.

**Abilita conversioni AutoCAD basate su Acrobat (solo Windows):** Quando questa impostazione è true, il servizio Generate PDF utilizza Acrobat per tutte le conversioni da DWG a PDF. Questa impostazione è utile solo se AutoCAD non è installato sul server o se il meccanismo di conversione AutoCAD non è in grado di convertire i file.

**Espressioni Regolari Per La Ricerca Di Speciali Proibiti
Caratteri nel nome utente (solo Windows):** Specifica i caratteri che interferiscono con le operazioni di Export PDF e Optimize PDF quando i caratteri vengono visualizzati nel nome di un utente.

**Dimensioni pool ImageToPDF:** dimensioni del pool del convertitore immagine-PDF predefinito (Java puro) nel servizio Generate PDF. Questa impostazione controlla le conversioni simultanee massime da immagine a PDF che il servizio Genera PDF può eseguire. Il valore predefinito di questa impostazione (consigliato per i sistemi a processore singolo) è 3, che può essere aumentato nei sistemi a più processori.

**Dimensione pool HTML-PDF:** dimensione pool del convertitore HTML-PDF nel servizio Generate PDF. Questa impostazione consente di controllare il numero massimo di conversioni HTML-PDF simultanee che il servizio Genera PDF può eseguire. Il valore predefinito di questa impostazione (consigliato per i sistemi a processore singolo) è 3, che può essere aumentato nei sistemi a più processori.

**Dimensioni pool OCR:** Dimensioni del pool di PaperCaptureService utilizzato da PDF Generator per OCR. Il valore predefinito di questa impostazione (consigliato per i sistemi a processore singolo) è 3, che può essere aumentato nei sistemi a più processori. Questa impostazione è valida solo nei sistemi Windows.

**Numero massimo di pagine ImageToPDF in memoria per le conversioni TIFF:** Questa impostazione determina il numero massimo di pagine da un&#39;immagine TIFF che possono rimanere in memoria prima di essere scaricate su disco durante la conversione in PDF. Il valore predefinito per questa impostazione è 500, che può essere aumentato se al processo di conversione ImageToPDF viene allocata memoria aggiuntiva.

**Famiglia di font di fallback per conversioni da HTML a PDF:** nome della famiglia di font da utilizzare nei documenti PDF quando il font utilizzato nel HTML originale non è disponibile in AEM Forms Server. Specificare una famiglia di tipi di carattere se si prevede di convertire le pagine HTML che utilizzano tipi di carattere non disponibili. Ad esempio, le pagine create in lingue regionali potrebbero utilizzare font non disponibili.

**Logica per nuovi tentativi per conversioni native** gestisce i nuovi tentativi di generazione di PDF se il primo tentativo di conversione non è riuscito:

* **Nessun nuovo tentativo**

  Non ritentare la conversione PDF se il primo tentativo di conversione non è riuscito

* **Riprova**

  Ritenta la conversione di PDF indipendentemente dal raggiungimento della soglia di timeout. La durata di timeout predefinita per il primo tentativo è di 270 secondi.

* **Riprova se il tempo lo consente**

  Ritenta conversione PDF se il tempo impiegato per il primo tentativo di conversione è inferiore alla durata di timeout specificata. Ad esempio, se la durata del timeout è di 270 secondi e il primo tentativo ha consumato 200 secondi, PDF Generator ritenterà la conversione. Se il primo tentativo ha consumato 270 secondi, la conversione non verrà ritentata.

## Guide ES4 Utilità impostazioni del servizio {#guides-es4-utilities-service-settings}

Quando si crea una Guida TV, alcune risorse, ad esempio la definizione della Guida TV, sono incorporate nella Guida TV. Le risorse possono anche esistere come riferimenti a risorse dell’applicazione memorizzate localmente o sul server AEM Forms. La Guida non contiene dati e i valori per la posizione di invio e gli input non sono adatti a tutti gli ambienti esterni.

Nella maggior parte dei casi, i servizi di rendering delle Guide predefiniti sono sufficienti per preparare una Guida da utilizzare in Workspace o in altri ambienti esterni. Nella vista Servizi, in Workbench, il servizio predefinito è Guide (sistema)/Processi/Guida rendering - 1.0. Il servizio Utilità guida ( `GuidesUtility`) consente di creare un processo personalizzato per il rendering di una guida, se necessario.

Le operazioni di Utilità guida (Guide Utilities) consentono di aggiungere le seguenti attività di rendering della Guida (Guide) a un processo:

* Determinare se i dati sono disponibili per compilare la Guida TV con
* Incorporare i dati della Guida TV o convertirli in un collegamento
* Convertire il contenuto di riferimento in URL accessibili esternamente
* Sostituire i valori in un documento HTML o in un altro wrapper o convertirli in URL accessibili esternamente
* Impostare la posizione di invio
* Specificare i valori di input
* Crea un parametro per rappresentare il contenuto a cui si fa riferimento
* Se sono disponibili varianti, imposta una variante

I valori predefiniti per il servizio Utilità guida supportano la maggior parte dei casi d&#39;uso. Tuttavia, se necessario, è possibile modificare i seguenti valori.

**publicPaths:** Questa opzione è stata dichiarata obsoleta. Non utilizzare questa opzione con i moduli AEM.

**pathInfoExpiryInSeconds:** l&#39;intervallo dopo il quale scade una richiesta di informazioni sul percorso da un client. Il valore predefinito è 1.

**collateralExpiryInSeconds:** L&#39;intervallo dopo il quale scade una richiesta di materiale promozionale da un client. Il valore predefinito è 315576000.

**mismatchExpiryInSeconds:** l&#39;intervallo dopo il quale scade una richiesta di materiale promozionale da un client, quando l&#39;eTag (tag di entità) non corrisponde. Un eTag è un’intestazione di risposta HTTP. Il valore predefinito è 1.

**guideContext:** radice del contesto dell&#39;applicazione Web Guide. Corrisponde al valore impostato utilizzando l’applicazione web Guide. Il valore predefinito è /Guides/.

**secureRandomAlgorithm:** algoritmo da utilizzare per la generazione di chiavi e identificatori. Questo valore viene passato al metodo getInstance della classe Java SecureRandom. Il valore predefinito è SHA1PRNG.

**idBytes:** numero di byte casuali da utilizzare per un identificatore di chiave. Il valore predefinito è 6.

**macAlgorithm:** algoritmo MAC (codice di autenticazione dei messaggi) da utilizzare per la verifica dell&#39;URL del materiale promozionale. Questo metodo viene passato al metodo getInstance della classe Mac. Il valore predefinito è HmacSHA1.

**macRefreshIntervalInMinutes:** il periodo di tempo in cui una chiave è attiva. Quando una chiave è attiva per questo intervallo, viene generata una nuova chiave. La nuova chiave diventa la chiave attiva. La chiave precedentemente attiva viene mantenuta per il 10% dell&#39;intervallo di aggiornamento. Questo comportamento consente agli URL generati utilizzando la chiave precedente di continuare a funzionare nello switch di chiave. Il valore predefinito è 144000.

**macOverlapIntervalInMinutes:** periodo di tempo durante il quale la chiave precedente rimarrà valida dopo la generazione di una nuova chiave. Il valore predefinito è 1440 minuti (1 giorno).

**macKeySeed:** Valore di inizializzazione per la generazione dell&#39;URL protetto. Quando questa è l’opzione, la chiave non viene mai aggiornata. Impostando lo stesso valore di inizializzazione su server diversi, questi server generano URL sicuri compatibili. Questo può essere utile se più server di moduli sono in uso dietro un load balancer. Immettete una sequenza casuale di caratteri e numeri come valore di partenza.

### Utilizzo delle guide in un cluster di server {#using-guides-in-a-server-cluster}

Il rendering di una guida in un cluster di server che non utilizza sessioni permanenti non riesce con un’eccezione NullPointerException. Una richiesta di Guide utilizza URL protetti che, per impostazione predefinita, sono univoci per il server su cui vengono generati. In un cluster che utilizza sessioni permanenti, dopo che una richiesta raggiunge un nodo nel cluster, tutte le richieste successive per tale sessione o utente vengono indirizzate esclusivamente a tale server e tutto va bene. In un cluster che non utilizza sessioni permanenti, le richieste successive possono raggiungere qualsiasi server del cluster. Se il server visitato dalle richieste non è il server originale, non viene risolto l’URL protetto.

Se si utilizzano Guide in un cluster di server che non utilizza sessioni permanenti, impostare il valore macKeySeed per il servizio GuidesUtility, quindi arrestare e avviare il cluster.

Il valore macKeySeed è il valore di inizializzazione del generatore di numeri casuali utilizzato per generare gli URL protetti. L’impostazione di questo valore fa sì che ogni nodo cluster inizializzi il generatore di numeri casuali nello stesso modo e abbia accesso agli stessi URL protetti. Puoi utilizzare qualsiasi stringa casuale per questo valore di seed.

Modifica il valore macKeySeed quando devi aggiornare gli URL protetti. L’aggiornamento degli URL protetti dipende dai criteri di sicurezza in uso ed è simile al criterio di aggiornamento per la modifica della password della directory principale principale del server. macSeedValue è analogo alla password master per gli URL protetti, in quanto viene utilizzato per generare un nuovo numero casuale univoco da utilizzare nella generazione e nel recupero sicuri degli URL.

Riavviare il cluster perché macSeedValue è di sola lettura all&#39;avvio del sistema. Tutti i nodi devono riavviare per leggere il valore, perché lo utilizzano in modo indipendente per inizializzare i numeri casuali interni con il valore di inizializzazione.

## Impostazioni servizio JDBC {#jdbc-service-settings}

Il servizio JDBC ( `JdbcService`) consente ai processi di interagire con i database.

Per il servizio JDBC è disponibile la seguente impostazione.

**datasourceName:** Valore stringa che rappresenta il nome JNDI dell&#39;origine dati da utilizzare per la connessione al server di database. L&#39;origine dati deve essere definita nel server applicazioni che ospita il server Forms. Il valore predefinito è il nome JNDI dell&#39;origine dati per il database dei moduli AEM.

## Impostazioni del servizio JMS {#jms-service-settings}

Il servizio JMS ( `JMS`) consente l&#39;interazione con i provider Java Messaging System (JMS) che implementano sia la messaggistica point-to-point che la messaggistica Publish/Subscribe.

Configurare il servizio JMS con le proprietà predefinite in modo che le operazioni del servizio possano connettersi e interagire con un provider JMS e un servizio JNDI associato. I valori delle proprietà del servizio sono impostati su valori predefiniti basati sul server applicazioni JBoss. Modificare questi valori se si utilizza un server applicazioni diverso per ospitare i moduli AEM.

Per il servizio JMS sono disponibili le seguenti impostazioni.

**URL provider:** URL del provider di servizi JNDI. Il valore predefinito è basato sul server applicazioni JBoss. I seguenti URL sono valori predefiniti per i server applicazioni supportati dai moduli AEM:

**JBoss:** `<server name>:1099`

**WebLogic:** `<server name>:7001`

**WebSphere:** `<server name>:2809`

**Nome utente JNDI:** Il nome utente dell&#39;account da utilizzare per l&#39;autenticazione con il provider di servizi JNDI utilizzato per la ricerca di nomi di coda e argomenti. Il valore predefinito è guest.

**Password JNDI:** La password associata al nome utente specificato per il nome utente JNDI. Il valore predefinito è guest.

**Fabbrica contesto iniziale:** classe Java da utilizzare come factory contesto iniziale. Il servizio JMS utilizza questa classe per creare un contesto iniziale, che è il punto di partenza per la risoluzione dei nomi di argomenti e code. Il valore predefinito è il context factory iniziale per il servizio JMS su JBoss. Le classi riportate di seguito sono le factory di contesto iniziali per i server applicazioni supportati da AEM forms.

**JBoss:** org.jnp.interfaces.NamingContextFactory

**WebLogic:** weblogic.jndi.WLInitialContextFactory

**WebSphere:** com.ibm.websphere.naming.WsnInitialContextFactory

**Nome utente connessione:** La password associata al nome utente specificato per il nome utente connessione. Il valore predefinito è guest.

**Password connessione:** La password associata al nome utente specificato per il nome utente della connessione. Il valore predefinito è guest.

**Altre proprietà:** coppie nome proprietà e valore che è possibile passare al provider di servizi JNDI. Queste proprietà dipendono dall’implementazione e dalla configurazione del provider in uso.

Le coppie nome proprietà e valore sono separate da punti e virgola **;**. Ad esempio, il testo seguente mostra il valore che verrebbe specificato per due proprietà denominate nome1 e nome2, con i valori valore1 e valore2, rispettivamente:

`name1=value1;name2=value2`

## Impostazioni servizio LDAP {#ldap-service-settings}

Il servizio LDAP ( `LDAPService`) fornisce le operazioni per l&#39;esecuzione di query sulle directory LDAP. Le directory LDAP vengono generalmente utilizzate per memorizzare informazioni sulle persone, i gruppi e i servizi di un&#39;organizzazione.

Per il servizio LDAP sono disponibili le seguenti impostazioni.

**Fabbrica contesto iniziale:** classe Java da utilizzare come context factory. Questa classe viene utilizzata per creare una connessione al server LDAP. Il valore predefinito è com.sun.jndi.ldap.LdapCtxFactory, appropriato per la maggior parte dei server LDAP.

**URL provider:** URL da utilizzare per la connessione al servizio LDAP. Il formato del valore è `ldap://server name:port`

*nome server* è il nome del computer che ospita il server LDAP

*porta* è la porta di comunicazione utilizzata dal servizio LDAP. Il valore predefinito è 389, che è la porta standard utilizzata per le connessioni LDAP.

**Nome utente:** Il nome utente dell&#39;account utente da utilizzare per accedere al server LDAP. L&#39;account utente deve disporre dell&#39;autorizzazione per connettersi al server e leggere le informazioni nella directory LDAP.

A seconda del server LDAP, il nome utente potrebbe essere un nome utente semplice come `myname` o un DN, come `cn=myname,cn=users,dc=myorg`.

**Password:** la password che corrisponde al nome utente fornito per l&#39;impostazione del nome utente.

**Altre proprietà:** Valore stringa che rappresenta altre proprietà e i valori corrispondenti che è possibile fornire al server LDAP. Il valore è nel formato seguente:

`property=value;property=value;...`

## Impostazioni del servizio di configurazione di Microsoft SharePoint {#microsoft-sharepoint-configuration-service-settings}

Il servizio di configurazione di Microsoft SharePoint `(MSSharePointConfigService)` consente di specificare le credenziali per l&#39;utente dei moduli AEM che dispone di autorizzazioni di rappresentazione. Per informazioni sulle autorizzazioni di rappresentazione, vedere [Configurazione del connettore per Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html).

Per il servizio di configurazione di Microsoft SharePoint sono disponibili le impostazioni seguenti:

* Nome utente per un utente con autorizzazioni di rappresentazione
* Password per l&#39;utente sopra indicato

**Abilita SSL (HTTPS):**

**Durata:** Durata in secondi della validità e della memorizzazione nella cache del profilo di provisioning. Il valore predefinito è 86400 (24 ore). Quando un&#39;applicazione client si sincronizza con il server e il tempo specificato è trascorso, l&#39;applicazione client richiede un nuovo profilo di provisioning dal server.

**Crittografia:** specifica se crittografare i dati archiviati nel dispositivo mobile.

**Applicazione Forms:** abilita la funzionalità Forms nelle applicazioni client per dispositivi mobili. Quando questa opzione è selezionata, gli utenti possono aprire i moduli e avviare i processi dai propri dispositivi mobili.

**Applicazione attività:** abilita la funzionalità Attività nelle applicazioni client mobili. Quando questa opzione è selezionata, gli utenti possono accedere ai propri elenchi di attività e completare attività dai propri dispositivi mobili.

**Applicazione Content Services:** abilita la funzionalità Content Services nell&#39;applicazione client mobile. Questa funzione è disponibile solo per iOS. Quando questa opzione è selezionata, gli utenti di iPhone e iPad possono accedere ai file memorizzati nel server WebDAV della propria organizzazione.

**Supporto offline:** consente agli utenti di continuare a utilizzare le applicazioni client per dispositivi mobili anche quando non dispongono di una connessione al server (ad esempio quando non sono in intervallo di celle o in modalità aereo). Gli utenti devono inoltre abilitare l’impostazione Offline Support sui propri dispositivi mobili. Questa funzione è disponibile per i dispositivi Android e iOS. Per impostazione predefinita, questa funzione è disattivata.

>[!NOTE]
>
>Se il supporto offline è stato abilitato e poi lo disattivi, i profili di provisioning degli utenti vengono aggiornati immediatamente o non appena sono online. Se un utente lavora in modalità non in linea, tutte le attività in sospeso vengono restituite al relativo elenco Attività e tutti gli elementi nella coda, inclusi i moduli in sospeso, le attività e i moduli contenenti errori di convalida, vengono eliminati dalla coda.

**Android:** consente ai dispositivi Android di connettersi al server.

**Apple iOS:** consente a iPhone e iPad di connettersi al server.

**AIR:** consente ai dispositivi che eseguono app basate su Adobe AIR® di connettersi al server.

**BlackBerry:** consente ai dispositivi BlackBerry di connettersi al server.

**Android Microsoft Exchange ActiveSync richiesto:** specifica se Microsoft Exchange ActiveSync Policy Manager (EA) deve essere installato e attivo sui dispositivi Android. Quando questa opzione è selezionata, l’EA deve essere applicato sul dispositivo Android. Se questa opzione non è selezionata, non viene eseguito alcun controllo, anche se vengono ancora applicati altri requisiti.

**Lunghezza minima PIN Android:** i dispositivi Android devono avere un&#39;impostazione globale che impone che il PIN o la password abbiano almeno questa lunghezza. Non è sufficiente disporre di un PIN della lunghezza specificata. La lunghezza del PIN deve essere imposta dal sistema in modo che gli utenti non possano rimuoverlo o accorciarlo in un secondo momento. Il valore predefinito è 4.

**Numero massimo di tentativi password Android prima della cancellazione:** I dispositivi Android hanno un&#39;impostazione globale che cancella il sistema dopo un numero specificato di tentativi di password non validi. Questa impostazione globale è abilitata ed è uguale o inferiore al valore specificato qui. Il valore predefinito è 5.

**Cancellazione Android alla rimozione:** specifica cosa accade quando si verifica una violazione dei criteri su un dispositivo Android. Quando questa opzione è selezionata, l’account viene eliminato. Se questa opzione non è selezionata, la password dell’account memorizzato e i dati memorizzati nella cache vengono eliminati. Non vengono più effettuati tentativi di sincronizzazione finché l’utente non corregge la violazione dei criteri.

## Impostazioni del servizio di output {#output-service-settings}

Il servizio di output `(OutputService)` consente di unire i dati del modulo XML con una struttura di modulo creata in Designer di moduli AEM per creare un flusso di output di documenti in uno dei seguenti formati:

* Flusso di output di un documento PDF o PDF/A.
* Un flusso di output di Adobe PostScript.
* Flusso di output PCL (Printer Control Language).
* Flusso di output Zebra Programming Language (ZPL).

Il flusso di output può essere inviato a una stampante di rete, a una stampante locale o a un file su disco. Quando utilizzi il servizio di output come parte di un processo, puoi anche inviare il flusso di output a un destinatario e-mail come allegato di un file.

Per il servizio Output sono disponibili le impostazioni seguenti.

**Tipo di transazione:** Specifica la modalità di propagazione di un contesto di transazione a un&#39;operazione:

**Obbligatorio:** supporta un contesto di transazione se ne esiste già uno; in caso contrario, viene creato un nuovo contesto di transazione. Questo è il valore predefinito.

**Richiede nuovo:** crea sempre un nuovo contesto di transazione. Se esiste un contesto di transazione attivo, viene sospeso.

**Timeout transazione (in sec):** il numero di secondi di attesa del provider di transazioni sottostante prima del rollback di una transazione che esegue il wrapping di questa operazione. Questo valore viene ignorato se viene propagato un contesto di transazione esistente.

Quando si elaborano file di dati di grandi dimensioni o si lavora su un server occupato, potrebbe essere necessario aumentare il timeout del servizio di output. Per modificare il valore di timeout, verificare che i server hardware dispongano di memoria adeguata e che la memoria sia disponibile per l&#39;heap di Java Application Server. Il valore predefinito è `180`.

## Impostazioni del servizio di configurazione PDFG {#pdfg-config-service-settings}

Le impostazioni seguenti sono disponibili per il servizio di configurazione PDFG ( `PDFGConfigService`).

**Directory opzioni processo utente:** il percorso della cartella del file system in cui il servizio C scrive i file delle opzioni del processo accessibili ad Acrobat Pro Extended. Il valore predefinito è [user.home]/Application Data/Adobe/Adobe PDF/Settings.

**Directory di avvio PS:** il percorso della cartella del file system in cui vengono salvati i file di avvio richiesti da Adobe Acrobat Distiller. Il valore predefinito è [user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**File di avvio PS:** Il nome del file di avvio richiesto da Adobe Acrobat Distiller. Il valore predefinito è example.ps.

**Timeout conversione server:** timeout massimo di conversione del processo (in secondi) per il servizio Generate PDF e il servizio Distiller. Questa impostazione limita il timeout massimo di conversione che può essere specificato nel file config.xml e nelle pagine della console di amministrazione di PDF Generator. Il valore predefinito è 270.

**Timeout globale del server:** Durante l&#39;esecuzione delle conversioni di PDF, un server Forms tiene conto del limite di timeout. Configura il valore di timeout per risolvere il problema.

**Prefisso opzioni processo:** Prefisso utilizzato dal servizio Generate PDF per anteporre una breve stringa ai file delle opzioni processo creati temporaneamente per l&#39;utilizzo da parte di Acrobat Distiller. Il valore predefinito è pdfg.

**App non Unicode:** un elenco separato da virgole di nomi di applicazioni che non supportano Unicode. Questo elenco è precompilato con i nomi di diverse applicazioni, il cui supporto è preconfigurato in PDF Generator. Se si sceglie di aggiungere il supporto per le conversioni PDF tramite altre applicazioni di terze parti che non supportano Unicode, è necessario aggiungerle a questo elenco. Il valore predefinito è Autocad,Excel,PowerPoint,Project,Publisher,Visio,Word,WordPerfect.

**Conteggio pool di thread del server:** Controlla le dimensioni del pool di thread utilizzato internamente dal servizio Generate PDF per soddisfare le richieste di conversione da HTML a PDF che implicano il spider (conversione di pagine collegate accessibili dalla pagina principale). Il valore predefinito è 20.

**Secondi analisi pulizia PDFG:** Per ulteriori dettagli, vedere la sezione Scadenze processo.

**Scadenza processo:** Il servizio Generate PDF elimina i file di input non appena vengono convertiti. Memorizza temporaneamente i file di output, per un periodo di tempo determinato dalle impostazioni Secondi analisi di pulizia PDFG e Secondi scadenza processo.

L&#39;impostazione Scadenza processo (secondi) specifica l&#39;età di un file o di una cartella vuota prima che sia possibile eliminarlo. L&#39;impostazione Scansione di pulizia PDFG Seconds specifica la frequenza con cui un thread di pulizia esegue la scansione delle cartelle temporanee per individuare i file che possono essere eliminati.

Ad esempio, se la proprietà Scadenza processo è impostata su 100 e la proprietà PDFG Cleanup Scan Seconds è impostata su 200, il thread di pulizia viene eseguito ogni 200 secondi ed elimina i file di almeno 100 secondi.

Il valore predefinito di Scansione pulizia PDFG in secondi è `43200` (12 ore). Il valore predefinito per Scadenza processo è `86400` (24 ore).

**Impostazioni locali predefinite:** Consente di ignorare le impostazioni locali predefinite (paese + lingua) del server in cui è distribuito il servizio Generate PDF. Se questo parametro non è specificato, le impostazioni internazionali predefinite vengono determinate in base al sistema operativo in cui il servizio viene distribuito. Questo parametro controlla la lingua in cui i messaggi di errore vengono restituiti alle API.

## impostazioni del servizio Servizi dati del flusso di lavoro dei moduli {#forms-workflow-data-services-service-settings}

I servizi seguenti estendono i servizi dati ed espongono gli assembler utilizzati da Workspace per parlare con il server. Non modificare le opzioni di configurazione per questi servizi a meno che non sia stato richiesto dal supporto Adobe. Questi servizi non sono destinati all&#39;accesso diretto:

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## Impostazioni servizio remoto {#remoting-service-settings}

La maggior parte dei servizi è configurata in modo da potervi accedere tramite (obsoleto per i moduli AEM) i moduli AEM in remoto. Per informazioni su (Obsoleto per i moduli AEM) moduli AEM in remoto, vedere [Programmazione con moduli AEM](https://adobe.com/go/learn_aemforms_programming_63).

Per il servizio di comunicazione remota sono disponibili le impostazioni seguenti.

**Metodo di autenticazione client Flex:** Determina il tipo di risposta che il server invia al client quando il servizio richiamato è abilitato per la sicurezza, l&#39;operazione richiamata non supporta chiamate anonime e il client trasmette credenziali non valide o non valide. Scegli tra Personalizzato o Base. Il valore predefinito è Base.

**Consenti la serializzazione delle classi non serializzabili:** La maggior parte degli endpoint dei moduli AEM consente l&#39;utilizzo solo di classi serializzabili per la chiamata. Nelle versioni precedenti, l’endpoint remoto consentiva l’utilizzo di classi non serializzabili per le chiamate dai client basati su Flex. Per evitare una vulnerabilità di sicurezza descritta in APS11-15, questa funzione è stata modificata. Se si desidera continuare a utilizzare le classi non serializzabili con l&#39;endpoint remoto di Flex, selezionare questa casella di controllo.

## Impostazioni del servizio archivio {#repository-service-settings}

Il servizio Archivio ( `RepositoryService`) fornisce servizi di archiviazione e gestione delle risorse ai moduli AEM. Quando gli sviluppatori creano un’applicazione, possono distribuire le risorse nell’archivio anziché in un file system. Le risorse possono includere qualsiasi tipo di materiale collaterale, tra cui moduli XML, PDF forms (inclusi i moduli Acrobat), frammenti di moduli, immagini, profili, criteri, file SWF, file DDX, schemi XML, file WSDL e dati di test.

È possibile utilizzare il repository predefinito incluso nei moduli AEM oppure un repository di terze parti (EMC Documentum Content Server, IBM FileNet Content Manager o IBM Content Manager).

Il servizio del provider dell&#39;archivio è un delegato del servizio che funge da interfaccia per un servizio del provider. Questo consente di connettersi a un’API comune e di non dover essere a conoscenza di quale servizio provider sta implementando le funzionalità di archiviazione. Il servizio Provider repository fornisce l&#39;archiviazione del database per le risorse del servizio repository.

Per il servizio Archivio è disponibile la seguente impostazione.

**Provider Service:** il nome del servizio utilizzato come provider di archiviazione. Il valore predefinito è RepositoryProviderService.

## Impostazioni del servizio di firma {#signature-service-settings}

Il servizio di firma ( `SignatureService`) consente all&#39;organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF distribuiti e ricevuti. Questo servizio utilizza le firme digitali e la certificazione per garantire che i documenti non vengano modificati. La modifica di un documento ne interrompe la firma. Poiché le funzioni di protezione vengono applicate al documento stesso, il documento rimane protetto e controllato per l&#39;intero ciclo di vita, oltre il firewall, quando viene scaricato offline e quando viene inviato nuovamente all&#39;organizzazione.

Per il servizio Firma sono disponibili le impostazioni seguenti.

**Nome del servizio SPI HSM remoto:** Questa opzione è da utilizzare quando HSM è installato in un computer remoto. Specificare questa opzione quando i moduli AEM sono installati in un sistema Windows a 64 bit e si utilizzano dispositivi HSM per la firma.

**URL del servizio Web HSM remoto:** Specificare questa opzione quando i moduli AEM sono installati in Windows a 64 bit e si utilizzano dispositivi HSM per la firma.

**Certificazione per includere le modifiche al caricamento del modulo:** Quando questa opzione è selezionata, oltre al modello XFA viene certificato anche lo stato del modulo XFA. L’abilitazione di questa opzione potrebbe avere un impatto negativo sulle prestazioni. Il valore predefinito è true.

**Esegui script Document JavaScript:** Specifica se eseguire gli script Document JavaScript durante le operazioni di firma. Il valore predefinito è false.

**Elabora documenti con compatibilità Acrobat 9:** Specifica se abilitare la compatibilità Acrobat 9. Ad esempio, quando questa opzione è selezionata, Certificazione visibile in PDF dinamici è abilitata. Il valore predefinito è false.

**Incorpora le informazioni di revoca durante la firma:** Specifica se le informazioni di revoca sono incorporate durante la firma del documento PDF. Il valore predefinito è false.

**Incorpora le informazioni di revoca durante la certificazione:** Specifica se le informazioni di revoca sono incorporate durante la certificazione del documento PDF. Il valore predefinito è false.

**Applica l&#39;incorporamento delle informazioni di revoca per tutti i certificati
Durante la firma/certificazione:** Specifica se un&#39;operazione di firma o certificazione non riesce se non sono incorporate informazioni di revoca valide per tutti i certificati. Si noti che se un certificato non contiene informazioni CRL o OCSP, viene considerato valido anche se non vengono recuperate informazioni di revoca. Il valore predefinito è false.

**Ordine di controllo delle revoche:** Specifica l&#39;ordine di controllo delle revoche quando il controllo è possibile tramite i meccanismi CRL (Certificate Revocation List) e OCSP (Online Certificate Status Protocol). Il valore predefinito è OCSPFirst.

**Dimensione massima delle informazioni di archiviazione della revoca:** La dimensione massima delle informazioni di archiviazione della revoca in kilobyte. L’AEM forma i tentativi di memorizzare quante più informazioni di revoca possibili senza superare il limite. Il valore predefinito è 10 KB.

**Firme Di Supporto Create Da Build PreRelease Di
Prodotti Adobe:** Quando questa opzione è selezionata, la firma creata con una versione non definitiva dei prodotti Adobe verrà convalidata correttamente. Il valore predefinito è false.

**Opzione ora di verifica:** Specifica l&#39;ora della verifica del certificato di un firmatario. Il valore predefinito è Ora di protezione diversa dall&#39;ora corrente.

**Utilizzare le informazioni di revoca archiviate nella firma durante
Convalida:** Specifica se le informazioni di revoca archiviate con la firma vengono utilizzate per il controllo della revoca. Il valore predefinito è true.

**Utilizzare Le Informazioni Di Convalida Memorizzate Nel Documento Per
Convalida delle firme:** Quando questa opzione è selezionata, per convalidare le firme vengono utilizzate le informazioni di convalida (incluse le informazioni di revoca e timestamp) incorporate nel documento. Il valore predefinito è true.

**Numero massimo di sessioni di verifica nidificate consentite:** Numero massimo di sessioni di verifica nidificate consentite. I moduli AEM utilizzano questo valore per impedire un ciclo infinito durante la verifica dei certificati firmatari OCSP o CRL quando il certificato OCSP o CRL non è configurato correttamente. Il valore predefinito è 10.

**Sfasamento orario massimo per verifica:** Tempo massimo, in minuti, per la firma dopo il tempo di convalida. Se lo sfasamento dell&#39;orologio è maggiore di questo valore, la firma non sarà valida. Il valore predefinito è 65 minuti.

**Cache durata certificato:** la durata di un certificato, recuperato online o tramite altri mezzi, nella cache. Il valore predefinito è 1 giorno.

### Opzioni di trasporto {#transport-options}

**Host proxy:** URL dell&#39;host proxy. Utilizzato solo se viene fornito un valore valido. Nessun valore predefinito.

**Porta proxy:** Porta proxy. Digitare un numero di porta valido compreso tra 0 e 65535. Il valore predefinito è 80.

**Nome utente di accesso proxy:** Nome utente di accesso proxy. Utilizzato solo se viene fornito un valore valido per l&#39;host proxy e la porta proxy. Nessun valore predefinito.

**Password di accesso proxy:** La password di accesso proxy. Utilizzato solo se viene fornito un valore valido per l&#39;host proxy, la porta proxy e il nome utente di accesso proxy. Nessun valore predefinito.

**Limite massimo di download:** la quantità massima di dati, in MB, che può essere ricevuta per connessione. Il valore minimo è 1 MB e il valore massimo è 1024 MB. Il valore predefinito è 16 MB.

**Timeout connessione:** il tempo massimo di attesa, in secondi, per stabilire una nuova connessione. Il valore minimo è 1 e il valore massimo è 300. Il valore predefinito è 5.

**Timeout socket:** il tempo massimo di attesa, in secondi, prima del timeout del socket (durante l&#39;attesa del trasferimento dei dati). Il valore minimo è 1 e il valore massimo è 3600. Il valore predefinito è 30.

### Opzioni di convalida del percorso {#path-validation-options}

**Richiedi criterio esplicito:** Specifica se il percorso deve essere valido per almeno uno dei criteri dei certificati associati al trust anchor del certificato del firmatario. Il valore predefinito è false.

**Inibisci qualsiasi criterio:** Specifica se l&#39;identificatore dell&#39;oggetto dei criteri (OID) deve essere elaborato se è incluso in un certificato. Il valore predefinito è false.

**Inibisci mapping criteri:** Specifica se il mapping dei criteri è consentito nel percorso di certificazione. Il valore predefinito è false.

**Controlla tutti i percorsi:** Specifica se tutti i percorsi devono essere convalidati o se la convalida deve essere interrotta dopo aver trovato il primo percorso valido. Seleziona true o false. Il valore predefinito è false.

**Server LDAP:** Server LDAP utilizzato per cercare i certificati per la convalida del percorso. Nessun valore predefinito.

**Segui URI in AIA certificato:** Specifica se gli URI (Uniform Resource Identifiers) in AIA certificato vengono elaborati durante l&#39;individuazione del percorso. Il valore predefinito è false.

**Estensione dei vincoli di base richiesta nei certificati CA:** Specifica se l&#39;estensione del certificato dei vincoli di base dell&#39;autorità di certificazione (CA) deve essere presente per i certificati CA. Alcuni primi certificati radice certificati tedeschi (7 e precedenti) non sono conformi alla RFC 3280 e non contengono l&#39;estensione del vincolo di base. Se si sa che il certificato EE di un utente è concatenato fino a una radice tedesca di questo tipo, deselezionare questa casella di controllo. Il valore predefinito è true.

**Richiedi firma del certificato valida durante la creazione della catena:** Specifica se il generatore di catene richiede firme valide per i certificati utilizzati per la creazione delle catene. Quando questa casella di controllo è selezionata, il generatore di catene non crea catene con firme RSA non valide nei certificati. Considerare la catena CA > ICA > EE se la firma della CA su un ICA non è valida. Se questa impostazione è true, la costruzione della catena si fermerà all&#39;ICA e l&#39;autorità di certificazione non verrà inclusa nella catena. Se questa impostazione è false, viene prodotta la catena completa di 3 certificati. Questa impostazione non influisce sulle firme DSA. Il valore predefinito è false.

### Opzioni provider marca temporale {#timestamp-provider-options}

**URL del server TSP:** URL del provider di timestamp predefinito. Utilizzato solo se viene fornito un valore valido. Nessun valore predefinito.

**Nome utente server TSP:** Il nome utente, se necessario, dal provider di timestamp. Utilizzato solo se viene fornito un valore valido per l’URL. Nessun valore predefinito.

**Password del server TSP:** la password per il nome utente indicato, se necessario, dal provider di timestamp. Utilizzato solo se viene fornito un valore valido per l’URL e il nome utente. Nessun valore predefinito.

**Algoritmo hash richiesta:** Specifica l&#39;algoritmo hash da utilizzare durante la creazione della richiesta per il provider di timestamp. Il valore predefinito è SHA1.

**Stile controllo revoca:** Specifica lo stile di controllo della revoca utilizzato per determinare lo stato di attendibilità del certificato del provider del timestamp in base allo stato di revoca osservato. Il valore predefinito è BestEffort.

**Invia Nonce:** Specifica se un nonce viene inviato con la richiesta del provider timestamp. Un nonce può essere una marca temporale, un contatore di visite su una pagina web o un marcatore speciale che ha lo scopo di limitare o impedire la riproduzione o la riproduzione non autorizzate di un file. Il valore predefinito è true.

**Usa marche temporali scadute durante la convalida:** Se questa opzione è selezionata, è possibile utilizzare marche temporali scadute per recuperare i tempi di convalida delle firme. Il valore predefinito è true.

**Dimensione risposta TSP:** Dimensione stimata, in byte, della risposta TSP. Questo valore deve rappresentare la dimensione massima della risposta del timestamp che il provider del timestamp configurato può restituire. Non modificare questa impostazione a meno che non si sia assolutamente sicuri. Il valore minimo è 60B e il valore massimo è 10240B. Il valore predefinito è 4096B.

**Ignora estensione server marca temporale**: selezionare l&#39;opzione **Ignora estensione server marca temporale** per impedire al server AEM Forms di contattare il server marca temporale specificato. La selezione dell’opzione consente di evitare errori di processo che si verificano a causa del timeout di connessione tra i server di AEM Forms e di marca temporale.

### Opzioni elenco revoche certificati {#certificate-revocation-list-options}

**Consultare prima l&#39;URI locale:** Specifica se la posizione CRL specificata nell&#39;URI locale o nella ricerca CRL deve avere la preferenza rispetto a qualsiasi posizione specificata in un certificato ai fini della verifica delle revoche. Il valore predefinito è false.

**URI locale per la ricerca CRL:** URL del provider CRL locale. Questo valore viene visualizzato solo se l&#39;impostazione Consulta URI locale per primo è impostata su true. Nessun valore predefinito.

**Stile controllo revoca:** Specifica lo stile di controllo della revoca utilizzato per determinare lo stato di attendibilità del certificato del provider CRL in base allo stato di revoca osservato. Il valore predefinito è BestEffort.

**Server LDAP per ricerca CRL:** Server LDAP utilizzato per ottenere i CRL (come www.ldap.com). Tutte le query basate su DN per i CRL verranno indirizzate a questo server. Nessun valore predefinito.

**Vai online:** specifica se andare online per recuperare un CRL. Se false, vengono consultati solo i CRL memorizzati nella cache (sul disco locale o quelli incorporati con la firma). Il valore predefinito è true.

**Ignora date validità:** Specifica se ignorare gli orari thisUpdate e nextUpdate della risposta, impedendo a questi orari di avere un effetto negativo sulla validità della risposta. Il valore predefinito è false.

**Richiedi estensione AKI nel CRL:** Specifica se l&#39;estensione Identificatore chiave di autorità deve essere inclusa in un CRL. Il valore predefinito è false.

### Opzioni del protocollo di stato del certificato in linea {#online-certificate-status-protocol-options}

**URL server OCSP:** URL per il server OCSP predefinito. L&#39;utilizzo del server OCSP specificato tramite questo URL dipende dall&#39;impostazione dell&#39;opzione URL da consultare. Nessun valore predefinito.

**URL da consultare Opzione:** Controlla l&#39;elenco e l&#39;ordine dei server OCSP utilizzati per eseguire il controllo dello stato. Il valore predefinito è UseAIAInCert.

**Stile controllo revoca:** Specifica lo stile di controllo della revoca utilizzato durante la verifica del certificato del server OCSP. Il valore predefinito è CheckIfAvailable.

**Invia Nonce:** Specifica se un nonce viene inviato con la richiesta OCSP. Un nonce può essere una marca temporale, un contatore di visite su una pagina web o un marcatore speciale che ha lo scopo di limitare o impedire la riproduzione o la riproduzione non autorizzate di un file. Il valore predefinito è true.

**Tempo massimo sfasamento orario:** Sfasamento massimo consentito, in minuti, tra il tempo di risposta e l&#39;ora locale. Il valore minimo è 0 e il valore massimo è 2147483647 m. Il valore predefinito è 5m.

**Tempo di aggiornamento risposta:** Tempo massimo, in minuti, per il quale una risposta OCSP precostruita è considerata valida. Il valore minimo è 1 m e il valore massimo consentito è 2147483647. Il valore predefinito è 525600 (un anno).

**Firma richiesta OCSP:** Specifica se la richiesta OCSP deve essere firmata. Il valore predefinito è false.

**Alias credenziali firmatario richiesta:** Specifica l&#39;alias credenziali da utilizzare per la firma della richiesta OCSP se la firma è abilitata. Utilizzato solo se la firma della richiesta OCSP è abilitata. Nessun valore predefinito.

**Vai in linea:** Specifica se accedere in linea per eseguire il controllo della revoca. Il valore predefinito è true.

**Ignora gli orari thisUpdate e nextUpdate della risposta:** Specifica se ignorare gli orari thisUpdate e nextUpdate della risposta, impedendo a questi orari di avere un effetto negativo sulla validità della risposta. Il valore predefinito è false.

**Consenti estensione OCSPNoCheck:** Specifica se l&#39;estensione OCSPNoCheck è consentita nel certificato di firma della risposta. Il valore predefinito è true.

**Richiedi estensione CertHash OCSP ISIS-MTT:** specifica se nelle risposte OCSP deve essere inclusa un&#39;estensione hash della chiave pubblica del certificato. Il valore predefinito è false.

### Opzioni di gestione degli errori per il debug {#error-handling-options-for-debugging}

**Elimina cache certificati nella chiamata API successiva:** Specifica se rimuovere la cache certificati quando viene chiamata la successiva operazione del servizio di firma. Una volta richiamata l’operazione, questa opzione viene impostata nuovamente su false. Il valore predefinito è false.

**Elimina cache CRL nella chiamata API successiva:** Specifica se eliminare la cache CRL quando viene chiamata la successiva operazione del servizio di firma. Una volta richiamata l’operazione, questa opzione viene impostata nuovamente su false. Il valore predefinito è false.

**Rimuovi cache OCSP nella chiamata API successiva:** Specifica se rimuovere la cache OCSP quando viene chiamata la successiva operazione del servizio di firma. Una volta richiamata l’operazione, questa opzione viene impostata nuovamente su false. Il valore predefinito è false.

## Impostazioni del servizio Cartelle controllate {#watched-folder-service-settings}

Il servizio Cartelle controllate ( `WatchedFolder`) configura gli attributi comuni a tutti gli endpoint della cartella controllata. Fornisce inoltre valori predefiniti per gli endpoint della cartella controllata. (Vedi [Configurazione degli endpoint della cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).) Non viene richiamata da applicazioni client esterne o utilizzata nei processi creati in Workbench.

Per il servizio Cartella controllata sono disponibili le impostazioni seguenti.

**Espressione Cron:** Espressione cron utilizzata dal quarzo per pianificare il polling della directory di input.

**Conteggio ripetizioni:** il numero di volte in cui viene eseguito il polling della directory di input. Il conteggio di ripetizioni predefinito da utilizzare se questo valore non è specificato nella configurazione dell’endpoint. Il valore -1 indica l&#39;analisi indefinita della directory. Il valore predefinito è -1.

**Intervallo di ripetizione:** Il numero predefinito in secondi tra ciascun sondaggio. Questo valore viene utilizzato come intervallo di ripetizione a meno che non venga specificato un valore diverso nella configurazione dell’endpoint della cartella controllata. Il valore predefinito è 5. Per ulteriori informazioni, consulta la descrizione dell’impostazione Dimensione batch.

**Asincrono:** identifica il tipo di chiamata come asincrono o sincrono. I processi transitori e sincroni possono essere richiamati solo in modo sincrono. Il valore predefinito è asincrono.

**Tempo di attesa:** valore predefinito espresso in secondi dopo il quale i file vengono recuperati dalle cartelle di input. Se il file o la cartella è precedente al tempo specificato nel tempo di attesa, viene prelevato per l’elaborazione. Il valore predefinito è 0.

**Dimensione batch:** Il valore predefinito per il numero di file o cartelle elaborati per analisi. Il valore predefinito è 2.

Le impostazioni Intervallo di ripetizione e Dimensione batch determinano il numero di file che la cartella controllata può raccogliere in ogni scansione. La cartella controllata utilizza un pool di thread al quarzo per analizzare la cartella di input. Il pool di thread è condiviso con altri servizi. Se l&#39;intervallo di scansione è ridotto, i thread eseguono spesso la scansione della cartella di input. Se i file vengono rilasciati frequentemente nella cartella controllata, mantenere l&#39;intervallo di scansione ridotto. Se i file vengono eliminati raramente, utilizzare un intervallo di scansione più ampio in modo che gli altri servizi possano utilizzare i thread.

Se si elimina un grande volume di file, ingrandire la dimensione del batch. Ad esempio, se il servizio richiamato dall’endpoint della cartella controllata è in grado di elaborare 700 file al minuto e gli utenti rilasciano i file nella cartella di input alla stessa velocità, l’impostazione di Dimensione batch su 350 e Intervallo di ripetizione su 30 secondi migliorerà le prestazioni della cartella controllata senza incorrere troppo nel costo della scansione della cartella controllata.

Quando i file vengono rilasciati nella cartella controllata, vengono elencati i file nell’input, il che può ridurre le prestazioni se la scansione viene eseguita ogni secondo. L&#39;aumento dell&#39;intervallo di scansione può migliorare le prestazioni. Se il volume dei file da eliminare è piccolo, regolare di conseguenza le dimensioni del batch e l&#39;intervallo di ripetizione. Ad esempio, se vengono rilasciati 10 file al secondo, prova a impostare l’intervallo di ripetizione su 1 secondo e la dimensione batch su 10.

In una configurazione cluster, la dimensione batch per un endpoint di cartella controllata non viene scalata in più nodi cluster. Ad esempio, se la dimensione del batch è impostata su `2` per un cluster a due nodi e l&#39;opzione Limitazione è selezionata, i nodi elaborano i file collettivamente in batch di due invece che ogni nodo elabora due file alla volta.

**Sovrascrivi nomi di file duplicati:** Stringa booleana che specifica se i nomi di file dei risultati duplicati vengono sovrascritti dalla cartella controllata e se i documenti conservati con lo stesso nome devono essere sovrascritti.

**Mantieni cartella:** Il valore predefinito per la cartella. Questa cartella viene utilizzata per copiare i file di origine in in caso di elaborazione corretta dell’input. Questo valore può essere un percorso vuoto, relativo o assoluto con un modello di file come descritto per l&#39;impostazione Cartella risultati.

**Cartella errori:** il nome della cartella in cui vengono copiati i file degli errori. Questo valore può essere un percorso vuoto, relativo o assoluto con un modello di file come descritto per l&#39;impostazione Cartella risultati.

**Cartella risultati:** Il nome predefinito per la cartella dei risultati. Questa cartella viene utilizzata per copiare i file dei risultati in. Questo valore può essere un percorso vuoto, relativo o assoluto con il seguente pattern di file.

* %F = prefisso nome file
* %E = estensione del nome file
* %Y = anno (completo)
* %y = anno (ultime due cifre)
* %M = mese
* %D = giorno del mese
* %d = giorno dell&#39;anno
* %H = ora (24 ore)
* %h = ora (12 ore)
* %m = minuto
* %s = secondo
* %l = millisecondi
* %R = numero casuale da 0 a 9
* %P = ID processo o processo

Ad esempio, se sono le 20:00 del 17 luglio 2009 e si specifica `C:/Test/WF0/failure/%Y/%M/%D/%H/`, la cartella dei risultati sarà `C:/Test/WF0/failure/2009/07/17/20`.

Se il percorso non è assoluto ma relativo, la cartella viene creata all’interno della cartella controllata. Per ulteriori informazioni sui modelli di file, vedere [Informazioni sui modelli di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Minore è la dimensione delle cartelle dei risultati, migliori saranno le prestazioni della cartella controllata. Ad esempio, se il carico stimato per la cartella controllata è di 1000 file all&#39;ora, provare uno schema come `result/%Y%M%D%H` in modo che venga creata una nuova sottocartella ogni ora. Se il caricamento è più piccolo (ad esempio, 1000 file al giorno), puoi utilizzare un pattern come `result/%Y%M%D`.

**Cartella stage:** Il nome predefinito per la cartella stage all&#39;interno della cartella controllata.

**Cartella di input:** Il nome predefinito per la cartella di input all&#39;interno della cartella controllata.

**Mantieni in caso di errore:** Se true, i file originali vengono conservati nella cartella degli errori in caso di errore.

**Limitazione:** Quando questa opzione è selezionata, limita il numero di processi delle cartelle controllate che l&#39;AEM elabora in un dato momento. Il valore Dimensione batch determina il numero massimo di processi (vedere Informazioni sulla limitazione).

## Impostazioni servizio Web {#web-service-service-settings}

Il servizio Web ( `WebService`) consente ai processi di richiamare le operazioni del servizio Web.

Il servizio Web consente ai processi di richiamare le operazioni del servizio Web. Ad esempio, un’organizzazione potrebbe voler integrare un processo per memorizzare e recuperare informazioni quali i dettagli di contatto e account richiamando i servizi web esposti di un fornitore di servizi. Il servizio Web richiama un servizio Web specificato e trasmette i valori per ciascuno dei relativi parametri. Quindi salva i valori restituiti dall’operazione in una variabile designata all’interno di un processo.

Il servizio Web interagisce con i servizi Web inviando e ricevendo messaggi SOAP. Il servizio supporta inoltre l&#39;invio di allegati MIME, MTOM e SwaRef con messaggi SOAP tramite il protocollo WS-Attachment. Le interazioni del servizio Web sono compatibili con i sistemi SAP e i servizi Web .NET.

Per il servizio Web sono disponibili le impostazioni seguenti.

**Archivio chiavi:** il percorso completo del file del keystore contenente la chiave privata da utilizzare per l&#39;autenticazione. Forms Server deve essere in grado di accedere al file.

**Password archivio chiavi:** la password per il file del registro chiavi.

**Tipo di archivio chiavi:** Il tipo di archivio chiavi. Non fornire alcun valore per utilizzare il tipo di keystore predefinito configurato per la JVM che esegue il server Forms. In caso contrario, fornisci uno dei seguenti valori:

* jks
* pkcs12
* cms
* imbrogli

**Archivio fonti attendibili:** Percorso completo del file dell&#39;archivio fonti attendibili contenente la chiave pubblica del server del servizio Web.

**Password archivio fonti attendibili:** La password per il file TrustStore.

**Tipo di archivio fonti attendibili:** Il tipo del truststore. Non fornire alcun valore per utilizzare il tipo di keystore predefinito configurato per la JVM che esegue il server Forms. In caso contrario, fornisci uno dei seguenti valori:

* jks
* pkcs12
* cms
* imbrogli

## Impostazioni del servizio di trasformazione XSLT {#xslt-transformation-service-settings}

Il servizio di trasformazione XSLT ( `XSLTService`) consente ai processi di applicare trasformazioni XSLT (Extensible Stylesheet Language Transformations) ai documenti XML.

Per il servizio Trasformazione XSLT è disponibile l&#39;impostazione seguente.

**Nome factory:** nome completo della classe Java da utilizzare per l&#39;esecuzione delle trasformazioni XSLT. Se non viene specificato alcun valore, viene utilizzata la factory predefinita configurata nella Java Virtual Machine che esegue il server Forms.

## Modifica delle impostazioni di protezione per un servizio {#modifying-security-settings-for-a-service}

Forms Server consente di configurare le impostazioni di protezione per ogni servizio, consentendo di configurare un controllo dell&#39;accesso dettagliato a livello di servizio.

Vengono installati i profili di sicurezza predefiniti, che possono essere configurati per soddisfare le esigenze del sistema. A ciascun profilo di sicurezza è associato un dominio e viene creato a livello di utente o di gruppo.

### Modificare le impostazioni di protezione per un servizio {#modify-security-settings-for-a-service}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizio fare clic sul servizio da configurare.
1. Fare clic sulla scheda Protezione.
1. Nell&#39;elenco Richiedi autenticazione chiamanti selezionare Sì o No per specificare se il servizio può essere richiamato con o senza credenziali.

   Se si seleziona Sì, il chiamante del servizio deve essere autenticato e l&#39;entità utente principale per quel chiamante deve essere autorizzata a richiamare il servizio. In caso contrario, il tentativo di chiamata verrà rifiutato.

   Se si seleziona No, il chiamante del servizio potrebbe essere autenticato o meno. La chiamata del servizio avrà sempre esito positivo perché non è presente alcun controllo di autorizzazione.

1. Per i servizi che contengono una o più operazioni contrassegnate per l&#39;accesso anonimo, selezionare o deselezionare Accesso anonimo consentito. Quando è abilitato l’accesso anonimo, qualsiasi utente all’interno del sistema può richiamare le operazioni sul servizio. Se l&#39;accesso anonimo è disabilitato, agli utenti deve essere concessa l&#39;autorizzazione per chiamare il servizio e richiamare le operazioni. Queste autorizzazioni vengono concesse agli utenti direttamente o come parte di un gruppo che le dispone.
1. Per alcuni servizi, l&#39;account utente che esegue l&#39;operazione influisce sui risultati. Ad esempio, in Content Services (Obsoleto), l’utente che memorizza il contenuto diventa il proprietario del contenuto, il che influisce su chi può successivamente accedere al contenuto. Se si utilizza un processo per archiviare il contenuto, è opportuno considerare quale utente viene utilizzato per eseguire il servizio di gestione dei documenti, in quanto l&#39;utente sarà proprietario del contenuto memorizzato.

   Per specificare l&#39;identità di runtime utilizzata da un servizio per eseguire operazioni, selezionare Specifica RunAs, selezionare un&#39;opzione dall&#39;elenco associato e quindi fare clic su Salva. Scegli una delle seguenti opzioni:

   **Richiamo:** utilizza la stessa identità dell&#39;utente che ha richiamato il servizio.

   **Sistema:** utilizza l&#39;utente di sistema per eseguire il servizio con privilegi completi.

   **Utente con nome:** consente di eseguire il servizio come utente specifico. Quando si seleziona questa opzione, fare clic su Seleziona utente per visualizzare la pagina Seleziona utente principale, in cui è possibile cercare e selezionare l&#39;utente.

   Se non si seleziona Specifica RunAs, viene utilizzato il comportamento predefinito.

   >[!NOTE]
   >
   >I servizi di rendering e invio utilizzati con xfaForm, Document Form e variabili Form vengono sempre eseguiti utilizzando l’account utente System.

1. Fare clic su Aggiungi entità per specificare le autorizzazioni di utenti e gruppi per questo servizio.
1. Nella schermata Seleziona entità vengono visualizzati gli utenti e i gruppi configurati in Gestione utente. Se l’utente o il gruppo desiderato non è visualizzato, utilizza la funzione di ricerca per trovarlo. Fare clic sul nome di un utente o gruppo.
1. Nella schermata Aggiungi autorizzazioni, seleziona le autorizzazioni da assegnare all’utente o al gruppo per questo servizio:

   * **INVOKE_PERM:** Per richiamare tutte le operazioni nel servizio
   * **MODIFY_CONFIG_PERM:** Per modificare la configurazione di un servizio
   * **SUPERVISOR_PERM:** Per visualizzare i dati dell&#39;istanza di processo per un servizio creato da un processo
   * **START_STOP_PERM:** Per avviare e arrestare un servizio
   * **ADD_REMOVE_ENDPOINTS_PERM:** Per aggiungere, rimuovere e modificare endpoint per un servizio
   * **CREATE_VERSION_PERM:** Per creare una versione del servizio
   * **DELETE_VERSION_PERM:** Per eliminare una versione del servizio
   * **MODIFY_VERSION_PERM:** Per modificare una versione del servizio
   * **READ_PERM:** Per visualizzare il servizio
   * **PROCESS_OWNER_PERM:** Da utilizzare in una versione futura dei moduli AEM. Non utilizzare questa autorizzazione.
   * **SERVICE_MANAGER_PERM:** Da utilizzare in una versione futura dei moduli AEM. Non utilizzare questa autorizzazione.
   * **SERVICE_AGENT_PERM:** Da utilizzare in una versione futura dei moduli AEM. Non utilizzare questa autorizzazione.

1. Fai clic su Aggiungi.

### Rimuovere l’entità da un profilo di sicurezza {#remove-the-principal-from-a-security-profile}

1. Nella pagina Gestione servizio selezionare il servizio da configurare.
1. Fare clic sulla scheda **Protezione**, selezionare il profilo di protezione da rimuovere e fare clic su **Rimuovi**.

## Configurazione del pooling per un servizio {#configuring-pooling-for-a-service}

Ogni servizio può sfruttare le funzionalità di pooling per gestire le richieste di chiamata in ingresso. L&#39;utilizzo di un pool di servizi garantisce che le istanze del servizio vengano richiamate da un singolo thread alla volta e riutilizzate in più richieste di chiamata, con conseguente miglioramento delle prestazioni. È inoltre possibile utilizzare il pooling per specificare l&#39;opzione Maximum Asynchronous Service Instances, che consente ai servizi di limitare il numero di richieste gestite in parallelo.

### Abilita pooling {#enable-pooling}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizio fare clic sul servizio da configurare.
1. Fare clic sulla scheda Pooling.
1. Nell&#39;elenco Strategia di elaborazione richieste selezionare Istanze in pool per tutte le richieste.
1. Nella casella Dimensione pool istanza servizio iniziale immettere la dimensione iniziale del pool. Quando il servizio viene distribuito, questo numero viene utilizzato per determinare il numero di istanze di implementazione del servizio create e allocate al pool libero, in attesa di richieste di chiamata. In questo modo il contenitore del servizio può rispondere immediatamente alle richieste di chiamata senza dover prima inizializzare un&#39;istanza del servizio.
1. Nella casella Dimensione massima pool di istanze del servizio immettere il numero massimo di istanze nel pool per un determinato servizio. Questa impostazione consente di controllare il numero di thread che possono eseguire un determinato servizio in un determinato momento. Il valore predefinito è 0, che determina una dimensione del pool illimitata.
1. Nella casella Numero massimo di istanze del servizio asincrone immettere il numero massimo di istanze del pool che è possibile utilizzare per soddisfare le richieste asincrone in un determinato momento. Questa impostazione consente al servizio di limitare il numero di richieste che può gestire in parallelo.
1. Nella casella Timeout attesa chiamata immettere il numero di millisecondi di attesa per la disponibilità di un servizio per una richiesta di chiamata. Se non si specifica un valore per questa impostazione, il valore predefinito è 0 e non viene generato alcun tempo di attesa.
1. Fai clic su Salva.

### Rimuovi pooling {#remove-pooling}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizio fare clic sul servizio da configurare.
1. Fare clic sulla scheda Pooling.
1. Nell’elenco Strategia di elaborazione richieste, seleziona Nuova istanza per ogni richiesta o Singola istanza per tutte le richieste.

   **Istanza singola per tutte le richieste:** Un&#39;istanza del servizio viene creata e memorizzata nella cache quando la prima richiesta arriva nel contenitore. Ogni richiesta successiva a tale richiesta utilizza la stessa istanza del servizio per gestire la richiesta.

   **Nuova istanza per ogni richiesta:** Viene creata una nuova istanza di servizio per ogni chiamata ricevuta.

1. Fai clic su Salva.
