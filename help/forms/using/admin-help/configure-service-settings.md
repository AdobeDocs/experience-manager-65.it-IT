---
title: Configurare le impostazioni del servizio
description: Scopri come configurare le impostazioni del servizio. Puoi utilizzare la pagina Gestione servizi per configurare le impostazioni per ciascuno dei servizi che fanno parte di AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: a6a10ff0-6f4d-42df-9b4e-f98a53cf1806
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Workbench
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '10836'
ht-degree: 100%

---

# Configurare le impostazioni del servizio {#configure-service-settings}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Puoi utilizzare la pagina Gestione servizi per configurare le impostazioni per ciascuno dei servizi che fanno parte di AEM Forms. Le impostazioni disponibili variano a seconda del servizio configurato.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Interrompi il servizio prima di modificarlo. Consulta [Avvio e interruzione dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).
1. Fai clic sul nome del servizio da configurare.
1. Se il servizio dispone di una scheda Configurazione, utilizzala per modificare le impostazioni del servizio. Per ulteriori informazioni, consulta l’elenco dei collegamenti riportati di seguito.

   >[!NOTE]
   >
   >Non tutti i servizi elencati nella pagina Gestione servizi dispongono di una scheda Configurazione. Per i processi che hai creato, la scheda Configurazione viene visualizzata solo se hai aggiunto un parametro di configurazione al processo in Workbench. Consulta “Parametri di configurazione” nella [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_it).


1. Fai clic sulla scheda Sicurezza e definisci le impostazioni di sicurezza per il servizio. Consulta [Modifica delle impostazioni di sicurezza per un servizio](configure-service-settings.md#modifying-security-settings-for-a-service).
1. Se il servizio dispone di una scheda Endpoint, utilizzala per modificare le impostazioni dell’endpoint. Consulta [Gestione degli endpoint](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md).
1. Fai clic sulla scheda Pooling e definisci le impostazioni di pooling. Consulta [Configurazione del pooling per un servizio](configure-service-settings.md#configuring-pooling-for-a-service).
1. Fai clic su Salva per salvare le modifiche o su Annulla per eliminarle.
1. Seleziona la casella di controllo accanto al nome del servizio e fai clic su Avvia per riavviare il servizio.

## Impostazioni del servizio flusso di lavoro di auditing {#audit-workflow-service-settings}

Workbench consente di registrare le istanze del processo durante l’esecuzione e di riprodurle per osservare il comportamento del processo. Consulta la [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_it). Per risparmiare spazio sul file system del server Forms, puoi limitare la quantità di dati di registrazione del processo archiviati. Puoi configurare le seguenti proprietà del servizio flusso di lavoro di auditing ( `AuditWorkflowService`):

**maxNumberOfRecordingInstances:** il numero massimo di registrazioni archiviate. Quando viene memorizzato il numero massimo, la registrazione meno recente viene rimossa dal file system quando crei una nuova registrazione. Questa proprietà è utile se tendi a creare molte registrazioni e desideri rimuovere automaticamente le registrazioni precedenti. Il valore predefinito è 50.

**MaxNumberOfRecordingEntries:** il numero massimo di voci di dati che puoi archiviare per ogni registrazione. Le voci di dati sono informazioni sulle operazioni del processo. Per ogni esecuzione di un’operazione vengono memorizzate diverse voci, ad esempio se l’operazione è stata avviata, se l’operazione è stata completata e se il ciclo di lavorazione che porta all’operazione è stato completato. Questa proprietà è utile quando i processi possono includere molte esecuzioni di operazioni, ad esempio quando si verifica un ciclo infinito. Il valore predefinito è 50.

## Impostazioni del servizio moduli con codici a barre {#barcoded-forms-service-settings}

Il servizio moduli con codice a barre `(BarcodedFormsService)` estrae i dati del codice a barre dalle immagini scansionate. Il servizio accetta un modulo con codice a barre (TIFF o PDF) come input ed estrae la rappresentazione automatica dei dati codificati dal codice a barre.

Per il servizio moduli con codice a barre sono disponibili le seguenti impostazioni.

**Lettura a sinistra:** se selezionata, le immagini del codice a barre vengono scansionate orizzontalmente da destra verso sinistra.

**Lettura a destra:** se selezionata, le immagini del codice a barre vengono scansionate orizzontalmente da sinistra verso destra.

**Lettura in alto:** se selezionata, le immagini dei codici a barre vengono scansioante verticalmente dal basso verso l’alto.

**Lettura in basso:** se selezionata, le immagini dei codici a barre vengono scansionate verticalmente dall’alto verso il basso.

>[!NOTE]
>
>Per impostazione predefinita, vengono selezionate tutte le opzioni. Deseleziona un’opzione solo se sai con certezza che i codici a barre non verranno visualizzati in questo modo nei moduli.

**Percorso file di base:** il percorso del file rispetto al quale vengono risolti i parametri dei file di input e output batch per le operazioni Esegui processo file XML ed Esegui processo file semplice. Nelle configurazioni in cluster, il percorso del file di base deve essere una posizione condivisa del file system alla quale tutti i nodi del cluster hanno accesso in lettura/scrittura.

**Nome origine dati:** il nome dell’origine dati utilizzata per manutenere le informazioni sullo stato e sulla cronologia dei processi di elaborazione batch. L’origine dati specificata deve supportare le transazioni globali (XA).

## Impostazioni del servizio Central Migration Bridge (obsoleto) {#central-migration-bridge-service-settings}

Il servizio Central Migration Bridge (`CentralMigrationBridge`) richiama un sottoinsieme di funzionalità Adobe Central Pro Output Server (Central), che include i comandi JFMERGE, JFTRANS e XMLIMPORT. Le operazioni del servizio Central Migration Bridge consentono di riutilizzare le seguenti risorse Central nei moduli di AEM:

* progettazione modello (&amp;ast;.ifd)
* modelli di output (&amp;ast;.mdf)
* file di dati (&amp;ast; file .dat)
* file preambolo (&amp;ast; file .pre)
* file di definizione dati (&amp;ast;.tdf)

Per il servizio Central Migration Bridge è disponibile l’impostazione seguente.

**Directory di installazione centrale:** directory in cui è installato Adobe Central 5.7.

## Impostazioni del servizio Content Repository Connector per EMC Documentum {#content-repository-connector-for-emc-documentum-service-settings}

Il servizio Content Repository Connector per EMC Documentum (`EMCDocumentumContentRepositoryConnector`) consente di creare processi che interagiscono con i contenuti conservati in un archivio Documentum.

Per il servizio Content Repository Connector per EMC Documentum è disponibile la seguente impostazione.

**Percorso predefinito oggetto Asset Link:** porzione predefinita del percorso nell’archivio Documentum per la conservazione dell’oggetto Asset Link. Il percorso effettivo è costituito dal percorso predefinito e dalla posizione del modello per moduli nell’archivio di AEM Forms.

Ad esempio, se il percorso predefinito è impostato su `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects` e il modello per moduli è archiviato in una cartella `/Docbase/forms/`, l’oggetto Asset Link viene archiviato nella posizione seguente:

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

Il valore predefinito di questa impostazione è `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## Impostazioni del servizio Content Repository Connector per IBM FileNet {#content-repository-connector-for-ibm-filenet-service-settings}

Content Repository Connector per IBM FileNet consente di creare processi che interagiscono con il contenuto memorizzato in un archivio IBM FileNet.

L’impostazione seguente è disponibile per il servizio Content Repository Connector per IBM FileNet.

**Percorso predefinito oggetto Asset Link:** parte predefinita del percorso nell’archivio IBM FileNet per la conservazione dell’oggetto Asset Link. Il percorso effettivo è costituito dal percorso predefinito e dalla posizione del modello per moduli nell’archivio di AEM Forms.

Ad esempio, se il percorso predefinito è impostato su `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects` e il modello per moduli è conservato in una cartella `/Docbase/forms/`, l’oggetto Asset Link viene archiviato nella posizione seguente:

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

Il valore predefinito di questa impostazione è `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## Impostazioni servizio Converti PDF {#convert-pdf-service-settings}

Il servizio Converti PDF (`ConvertPdfService`) converte i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF). La conversione di un documento PDF in PostScript è utile per la stampa basata su server non monitorato su qualsiasi stampante PostScript. La conversione di un documento PDF in un file TIFF multipagina è pratica quando si archiviano documenti in sistemi di gestione dei contenuti che non supportano documenti PDF.

Per il servizio Converti PDF sono disponibili le impostazioni seguenti.

**Tipo di transazione:** specifica la modalità di propagazione di un contesto di transazione a un’operazione.

**Obbligatorio:** supporta un contesto di transazione, se ne esiste uno; in caso contrario, viene creato un nuovo contesto di transazione. Questo è il valore predefinito.

**Nuovo obbligatorio:** crea sempre un nuovo contesto di transazione. Se esiste un contesto di transazione attivo, viene sospeso.

**Timeout transazione (in sec):** il numero di secondi di attesa del provider di transazioni sottostante prima del rollback di una transazione che esegue il wrapping di questa operazione. Questo valore verrà ignorato se viene propagato un contesto di transazione esistente. Il valore predefinito è 180.

**Risoluzione di soglia per l’uniformità (in dpi):** la risoluzione dell’immagine al di sotto della quale l’uniformità (o l’antialiasing) viene applicata a testo, tratto e immagini, se hai selezionato le opzioni “Applica uniformità a” per tali elementi.

**Applica uniformità al testo:** controlla l’antialiasing del testo. Per disattivare l’uniformità del testo e renderlo più nitido e più semplice da leggere con un ingrandimento dello schermo, deseleziona questa casella di controllo.

**Applica uniformità a LineArt:** applica l’uniformità per rimuovere angoli improvvisi nelle linee.

**Applica uniformità alle immagini:** applica l’uniformità per ridurre al minimo le modifiche improvvise nelle immagini.

## Impostazioni servizio Distiller {#distiller-service-settings}

Il servizio Distiller (`DistillerService`) converte i file PostScript, Encapsulated PostScript (EPS) e PRN in file PDF in rete.

Per il servizio Distiller sono disponibili le impostazioni seguenti.

**Impostazioni di Adobe PDF:** le seguenti impostazioni preconfigurate vengono applicate al PDF generato:

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

**Impostazioni di protezione:** impostazioni di protezione preconfigurate applicate ai documenti PDF generati. Il valore predefinito è Nessuna protezione. Crea le impostazioni di protezione tramite PDF Generator, quindi inserisci le impostazioni qui.

**Dimensione del pool:** dimensione iniziale del pool. Quando il servizio Distiller viene distribuito, questo numero viene utilizzato per determinare il numero di istanze di implementazione del servizio create e allocate al pool libero in attesa di richieste di chiamata. Il contenitore del servizio può quindi rispondere immediatamente alle richieste di chiamata senza dover prima inizializzare un’istanza del servizio.

## Impostazioni del servizio di gestione dei documenti {#document-management-service-settings}

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulla persona. Il supporto di Content Services (obsoleto) termina il 31/12/2014. Consulta il [documento sul ciclo di vita del prodotto Adobe](https://helpx.adobe.com/it/support/programs/eol-matrix.html).

Il servizio di gestione dei documenti (`DocumentManagementService`) consente ai processi di utilizzare la funzionalità di gestione dei contenuti fornita da Content Services (obsoleto). Le operazioni di gestione dei documenti garantiscono le attività di base necessarie per mantenere spazi e contenuti nel sistema di gestione dei contenuti. Esempi di tali attività sono la copia, l’eliminazione, lo spostamento, il recupero e l’archiviazione dei contenuti, la creazione di spazi e associazioni, nonché l’ottenimento e l’impostazione degli attributi dei contenuti.

Per il servizio di gestione dei documenti sono disponibili le impostazioni seguenti.

**Schema dell’archivio:** schema dell’archivio in cui si trova il contenuto. Il valore predefinito è area di lavoro.

**Porta HTTP:** porta utilizzata per accedere a Content Services (obsoleta). Il valore predefinito è 8080.

## Impostazioni del servizio e-mail {#email-service-settings}

L’e-mail viene comunemente utilizzata per distribuire contenuti o fornire informazioni sullo stato come parte di un processo automatizzato. Il servizio e-mail (`EmailService`) consente ai processi di ricevere messaggi e-mail da un server POP3 o IMAP e di inviarne a un server SMTP.

Un processo, ad esempio, utilizza il servizio e-mail per inviare un messaggio e-mail con un modulo PDF in allegato. Il servizio e-mail si connette a un server SMTP per inviare il messaggio e-mail con l’allegato. Il modulo PDF è progettato per consentire al destinatario di fare clic su Invia dopo aver completato il modulo. L’azione fa sì che il modulo venga restituito come allegato al server e-mail designato. Il servizio e-mail recupera il messaggio e-mail restituito e archivia il modulo completato in una variabile del modulo dati del processo.

Per il servizio e-mail sono disponibili le seguenti impostazioni.

**Host SMTP:** indirizzo IP o URL del server SMTP da utilizzare per l’invio di e-mail.

**Numero della porta SMTP:** porta utilizzata per la connessione al server SMTP.

**Autenticazione SMTP:** da selezionare se per connettersi al server SMTP è necessaria l’autenticazione utente.

**Utente SMTP:** nome utente dell’account utente da utilizzare per accedere al server SMTP.

**Password SMTP:** password associata all’account utente SMTP.

**Protezione trasporto SMTP:** protocollo di protezione da utilizzare per la connessione al server SMTP:

* Seleziona Nessuno se non viene utilizzato alcun protocollo (i dati vengono inviati in formato testo in chiaro)
* Seleziona SSL se utilizzi il protocollo Secure Sockets Layer.
* Seleziona TLS se utilizzi Transport Layer Security.

**Host POP3/IMAP:** indirizzo IP o URL del server POP3 o IMAP da utilizzare per l’invio di messaggi e-mail.

**Nome utente POP3/IMAP:** il nome utente dell’account utente da utilizzare per accedere al server POP3 o IMAP.

**Password POP3/IMAP:** la password associata all’account utente POP3 o IMAP.

**Numero porta POP3/IMAP:** la porta utilizzata per la connessione al server POP3 o IMAP.

**POP3/IMAP:** il protocollo da utilizzare per l’invio e la ricezione delle e-mail.

**Ricevi sicurezza trasporto:** il protocollo di sicurezza da utilizzare per la connessione al server SMTP:

* Seleziona Nessuno se non utilizzi alcun protocollo (i dati vengono inviati in formato testo leggibile).
* Seleziona SSL se utilizzi il protocollo Secure Sockets Layer.
* Seleziona TLS se utilizzi Transport Layer Security.

## Impostazioni del servizio di crittografia {#encryption-service-settings}

Il servizio di crittografia ( `EncryptionService`) ti consente di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il relativo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l’accesso al contenuto. Se un documento PDF è crittografato con una password, l’utente deve specificare la password di apertura prima che il documento possa essere visualizzato in Adobe Reader o Adobe Acrobat. Analogamente, se un documento PDF è crittografato con un certificato, l’utente deve decrittografare il documento PDF con la chiave pubblica corrispondente al certificato (chiave privata) utilizzato per crittografare il documento PDF.

Per il servizio di crittografia sono disponibili le seguenti impostazioni.

**Server LDAP predefinito a cui connettersi:** il nome host del server LDAP utilizzato per recuperare i certificati per la crittografia dei documenti.

**Porta LDAP predefinita a cui connettersi:** il numero di porta del server LDAP.

**Nome utente LDAP predefinito:** se il server LDAP richiede l’autenticazione, specifica il nome utente da utilizzare per la connessione al server LDAP.

**Password LDAP predefinita:** se il server LDAP richiede l’autenticazione, specifica la password corrispondente al nome utente da utilizzare per la connessione al server LDAP.

>[!NOTE]
>
>Utilizza l’autenticazione semplice (nome utente e password) solo quando la connessione è protetta tramite SSL (utilizzando LDAPS).

<!-- **Compatibility Mode:**-->

## Impostazioni del servizio FTP {#ftp-service-settings}

Il servizio FTP ( `FTP`) consente ai processi di interagire con un server FTP. Le operazioni del servizio FTP possono recuperare file dal server FTP, inserirli nel server FTP ed eliminarli dal server FTP. Ad esempio, documenti come i rapporti generati da un processo possono essere memorizzati su un server FTP per la distribuzione. In alternativa, un sistema esterno può generare alcuni file in base ai passaggi precedenti di un processo. In un passaggio successivo del processo, i file possono essere trasferiti in una posizione remota.

Per il servizio FTP sono disponibili le seguenti impostazioni.

**Host predefinito:** l’indirizzo IP o l’URL del server FTP.

**Porta predefinita:** la porta utilizzata per la connessione al server FTP. Il valore predefinito è 21.

**Nome utente predefinito:** il nome dell’account utente che puoi utilizzare per accedere al server FTP. L’account utente deve disporre di privilegi sufficienti per eseguire le operazioni FTP richieste dal servizio.

**Password predefinita:** la password da utilizzare con il nome utente specificato per l’autenticazione con il server FTP.

## Impostazioni del servizio di generazione PDF {#generate-pdf-service-settings}

Il servizio di generazione PDF ( `GeneratePDFService`) converte i file in vari formati nativi in documenti PDF e converte i documenti PDF in diversi formati di file.

Per il servizio di generazione PDF sono disponibili le seguenti impostazioni.

**Impostazioni Adobe PDF:** il nome delle impostazioni Adobe PDF preconfigurate da applicare a un processo di conversione, se tali impostazioni non sono specificate come parte dei parametri di chiamata API. Le impostazioni Adobe PDF vengono configurate nella console di amministrazione facendo clic su Servizi > PDF Generator > Impostazioni Adobe PDF. Queste impostazioni sono applicabili solo alle conversioni basate su PDFMaker.

**Impostazioni sicurezza:** il nome delle impostazioni di sicurezza preconfigurate da applicare a un processo di conversione, se tali impostazioni non sono specificate come parte dei parametri di chiamata API. Le impostazioni di sicurezza vengono configurate nella console di amministrazione facendo clic su Servizi > PDF Generator > Impostazioni sicurezza.

**Impostazioni tipo di file:** il nome dell’impostazione tipo di file preconfigurata da applicare a un processo di conversione, se tali impostazioni non sono specificate come parte dei parametri di chiamata API. Le impostazioni tipo di file vengono configurate nella console di amministrazione facendo clic su Servizi > PDF Generator > Impostazioni tipo di file.

**Usa WebCapture (solo Windows):** quando questa impostazione è vero, il servizio di generazione PDF utilizza Acrobat per tutte le conversioni da HTML a PDF. Può migliorare la qualità dei file PDF prodotti da HTML, anche se le prestazioni possono essere leggermente inferiori. Il valore predefinito è falso.

**Convertitore principale per conversioni da HTML a PDF:** il servizio di generazione PDF fornisce più percorsi per la conversione di file HTML in documenti PDF: Webkit, WebCapture (solo Windows) e WebToPDF. Questa impostazione consente all’utente di selezionare il convertitore principale per convertire HTML in PDF. Per impostazione predefinita, è selezionato WebToPDF.

**Convertitore fallback per conversioni da HTML a PDF:** se il convertitore principale non riesce, specifica il convertitore per conversioni da HTML a PDF. Per impostazione predefinita, è selezionato WebCapture (solo Windows).

**Usa Acrobat Image Conversion (solo Windows):** quando questa impostazione è vero, il servizio di generazione PDF utilizza Acrobat per tutte le conversioni da immagine a PDF. Questa impostazione è utile solo se il meccanismo di conversione Java puro predefinito non è in grado di convertire correttamente una proporzione significativa delle immagini di input. Il valore predefinito è falso.

**Abilita conversioni AutoCAD basate su Acrobat (solo Windows):** quando questa impostazione è vero, il servizio di generazione PDF utilizza Acrobat per tutte le conversioni da DWG a PDF. Questa impostazione è utile solo se AutoCAD non è installato sul server o se il meccanismo di conversione AutoCAD non è in grado di convertire i file.

**Espressioni regolari per la ricerca di caratteri speciali
proibiti nel nome utente (solo Windows):** specifica i caratteri che interferiscono con le operazioni di Esporta PDF e Ottimizza PDF quando i caratteri vengono visualizzati nel nome di un utente.

**Dimensioni pool ImageToPDF:** le dimensioni pool del convertitore da immagine a PDF predefinito (Java puro) nel servizio di generazione PDF. Questa impostazione consente di controllare il numero massimo di conversioni simultanee da immagine a PDF che il servizio di generazione PDF può eseguire. Il valore predefinito di questa impostazione (consigliato per i sistemi a processore singolo) è 3, che puoi aumentare nei sistemi a più processori.

**Dimensioni pool da HTML a PDF:** le dimensioni pool del convertitore da HTML a PDF nel servizio di generazione PDF. Questa impostazione consente di controllare il numero massimo di conversioni simultanee da HTML a PDF che il servizio di generazione PDF può eseguire. Il valore predefinito di questa impostazione (consigliato per i sistemi a processore singolo) è 3, che puoi aumentare nei sistemi a più processori.

**Dimensioni pool OCR:** le dimensioni pool di PaperCaptureService utilizzato da PDF Generator per OCR. Il valore predefinito di questa impostazione (consigliato per i sistemi a processore singolo) è 3, che puoi aumentare nei sistemi a più processori. Questa impostazione è valida solo nei sistemi Windows.

**Numero massimo di pagine ImageToPDF in memoria per le conversioni TIFF:** questa impostazione determina il numero massimo di pagine da un’immagine TIFF che possono rimanere in memoria prima di essere scaricate su disco durante la conversione in PDF. Il valore predefinito per questa impostazione è 500, che puoi aumentare se al processo di conversione ImageToPDF viene allocata memoria aggiuntiva.

**Famiglia di font di fallback per conversioni da HTML a PDF:** il nome della famiglia di font da utilizzare nei documenti PDF quando il font utilizzato nell’HTML originale non è disponibile per il server AEM Forms. Specifica una famiglia di font se prevedi di convertire le pagine HTML che utilizzano font non disponibili. Ad esempio, le pagine create in lingue regionali potrebbero utilizzare font non disponibili.

**Logica di retry per conversioni native** gestisce i nuovi tentativi di generazione di PDF se il primo tentativo di conversione non è riuscito:

* **Nessun tentativo**

  Non riprova la conversione PDF se il primo tentativo di conversione non è riuscito

* **Riprova**

  Riprova la conversione PDF indipendentemente dal raggiungimento della soglia di timeout. La durata di timeout predefinita per il primo tentativo è di 270 secondi.

* **Riprova se il tempo a disposizione lo consente**

  Riprova la conversione PDF se il tempo impiegato per il primo tentativo di conversione è inferiore alla durata di timeout specificata. Ad esempio, se la durata di timeout è di 270 secondi e il primo tentativo ha consumato 200 secondi, PDF Generator riproverà la conversione. Se il primo tentativo ha consumato 270 secondi, la conversione non verrà riprovata.

## Impostazioni del servizio Utility per le Guide in ES4 {#guides-es4-utilities-service-settings}

Quando crei una guida, alcune risorse, ad esempio la definizione della guida, sono incorporate nella guida. Le risorse possono anche esistere come riferimenti a risorse dell’applicazione memorizzate localmente o sul server AEM Forms. La guida non contiene dati e i valori per la posizione di invio e gli input non sono adatti a tutti gli ambienti esterni.

Nella maggior parte dei casi, i servizi di rendering delle guide predefiniti sono sufficienti per preparare una guida da utilizzare in Workspace o in altri ambienti esterni. Nella vista Servizi, in Workbench, il servizio predefinito è Guide (sistema)/Processi/Guida rendering - 1.0. Il servizio Utility per le guide ( `GuidesUtility`) ti consente di creare un processo personalizzato per il rendering di una guida, se necessario.

Le operazioni di Utility per le guide ti consentono di aggiungere le seguenti attività di rendering della guida a un processo:

* Determinare se i dati sono disponibili per compilare la guida con
* Incorporare i dati della guida o convertirli in un collegamento
* Convertire il contenuto di riferimento in URL accessibili esternamente
* Sostituire i valori in un documento HTML o in un altro wrapper o convertirli in URL accessibili esternamente
* Impostare la posizione di invio
* Specificare i valori di input
* Creare un parametro per rappresentare il contenuto a cui si fa riferimento
* Se sono disponibili varianti, imposta una variante

I valori predefiniti per il servizio Utility per le guide supportano la maggior parte dei casi d’uso. Tuttavia, se necessario, puoi modificare i seguenti valori.

**publicPaths:** questa opzione è stata dichiarata obsoleta. Non utilizzare questa opzione con AEM Forms.

**pathInfoExpiryInSeconds:** l’intervallo dopo il quale una richiesta di informazioni scade sul percorso da un client. Il valore predefinito è 1.

**collateralExpiryInSeconds:** L’intervallo dopo il quale scade una richiesta di risorse ausiliarie da un client. Il valore predefinito è 315576000.

**mismatchExpiryInSeconds:** L’intervallo dopo il quale scade una richiesta di risorse ausiliarie da un client, quando l’eTag (tag di entità) non corrisponde. (Un eTag è un’intestazione di risposta HTTP.) Il valore predefinito è 1.

**guideContext:** La radice del contesto dell’applicazione web Guide. Corrisponde al valore impostato utilizzando l’applicazione web Guide. Il valore predefinito è /Guides/.

**secureRandomAlgorithm:** L’algoritmo da utilizzare per la generazione di chiavi e identificatori. Questo valore viene trasmesso al metodo getInstance della classe Java SecureRandom. Il valore predefinito è SHA1PRNG.

**idBytes:** numero di byte casuali da utilizzare per un identificatore chiave. Il valore predefinito è 6.

**macAlgorithm:** algoritmo MAC (codice di autenticazione dei messaggi) da utilizzare per la verifica dell’URL del materiale collaterale. Questo metodo viene passato al metodo getInstance della classe MAC. Il valore predefinito è HmacSHA1.

**macRefreshIntervalInMinutes:** il periodo di tempo in cui una chiave è attiva. Quando una chiave è stata attiva per questo intervallo, viene generata una nuova chiave. La nuova chiave diventa la chiave attiva. La chiave precedentemente attiva viene mantenuta per il 10% dell’intervallo di aggiornamento. Questo comportamento consente agli URL generati utilizzando la chiave precedente di continuare a funzionare nel passaggio da una chiave a un’altra. il valore predefinito è 144000.

**macOverlapIntervalInMinutes:** periodo di tempo durante il quale la chiave precedente rimarrà valida dopo la generazione di una nuova chiave. Il valore predefinito è 1440 minuti (1 giorno).

**macKeySeed:** un valore di seed per la generazione dell’URL protetto. Quando l’opzione è questa, la chiave non viene mai aggiornata. Impostando lo stesso seed su server diversi, questi server genereranno URL protetti e compatibili. Questo può essere utile se più server Forms sono in uso dietro un load balancer. Immetti una sequenza casuale di caratteri e numeri come seed.

### Utilizzo delle guide in un cluster di server {#using-guides-in-a-server-cluster}

Il rendering di una guida in un cluster di server che non utilizza sessioni permanenti non riesce e viene generata un’eccezione NullPointerException. Una richiesta delle Guide utilizza URL protetti che, per impostazione predefinita, sono univoci per il server su cui vengono generati. In un cluster che utilizza sessioni permanenti, dopo che una richiesta raggiunge un nodo nel cluster, tutte le richieste successive per tale sessione o utente vengono indirizzate esclusivamente a tale server e tutto va bene. In un cluster che non utilizza sessioni permanenti, le richieste successive possono raggiungere qualsiasi server del cluster. Se il server raggiunto dalle richieste non è il server originale, quelle non riescono a risolvere l’URL protetto.

Se utilizzi le Guide in un cluster di server che non utilizza sessioni permanenti, imposta il valore macKeySeed per il servizio GuidesUtility, quindi arresta e avvia il cluster.

Il valore macKeySeed è il seed per il generatore di numeri casuali utilizzato per generare gli URL protetti. L’impostazione di questo valore fa sì che ogni nodo del cluster inizializzi il generatore di numeri casuali nello stesso modo e abbia accesso agli stessi URL protetti. Puoi utilizzare qualsiasi stringa casuale per questo valore di seed.

Modifica il valore macKeySeed quando devi aggiornare gli URL protetti. L’aggiornamento degli URL protetti dipende dal criterio di protezione in uso ed è simile al criterio di aggiornamento per la modifica della password della directory principale del server. Il macSeedValue è analogo alla password principale per gli URL protetti, in quanto viene utilizzato per generare un nuovo numero casuale univoco da utilizzare nella generazione e nel recupero degli URL protetti.

Riavvia il cluster perché macSeedValue è di sola lettura all’avvio del sistema. Tutti i nodi devono essere riavviati per leggere il valore, perché lo utilizzano in modo indipendente per inizializzare i numeri casuali interni con il valore di seed.

## Impostazioni del servizio JDBC {#jdbc-service-settings}

Il servizio JDBC ( `JdbcService`) consente ai processi di interagire con i database.

Per il servizio JDBC è disponibile la seguente impostazione.

**datasourceName:** valore stringa che rappresenta il nome JNDI dell’origine dati da utilizzare per la connessione al server di database. L’origine dati deve essere definita nel server applicazioni che ospita il server Forms. Il valore predefinito è il nome JNDI dell’origine dati per il database di AEM Forms.

## Impostazioni del servizio JMS {#jms-service-settings}

Il servizio JMS ( `JMS`) consente l’interazione con i provider Java Messaging System (JMS) che implementano sia la messaggistica da punto a punto che la messaggistica publish/subscribe.

Configura il servizio JMS con le proprietà predefinite, in modo che le operazioni del servizio possano connettersi e interagire con un provider JMS e un servizio JNDI associato. I valori delle proprietà del servizio sono impostati su valori predefiniti basati sul server applicazioni JBoss. Modifica questi valori se utilizzi un altro server applicazioni per l’hosting di AEM Forms.

Per il servizio JMS sono disponibili le seguenti impostazioni.

**URL del provider:** URL del provider dei servizi JNDI. Il valore predefinito è basato sul server applicazioni JBoss. I seguenti URL sono valori predefiniti per i server applicazioni supportati da AEM Forms:

**JBoss:** `<server name>:1099`

**WebLogic:** `<server name>:7001`

**WebSphere:** `<server name>:2809`

**Nome utente JNDI:** nome utente dell’account da utilizzare per l’autenticazione con il provider di servizi JNDI utilizzato per la ricerca di nomi di coda e di argomenti. Il valore predefinito è guest.

**Password JNDI:** password associata al nome utente specificato in Nome utente JNDI. Il valore predefinito è guest.

**Factory del contesto iniziale:** classe Java da utilizzare come factory del contesto iniziale. Il servizio JMS utilizza questa classe per creare un contesto iniziale, che è il punto di partenza per la risoluzione di nomi di argomenti e code. Il valore predefinito è la factory del contesto iniziale per il servizio JMS su JBoss. Le classi riportate di seguito sono le factory del contesto iniziale per i server di applicazioni supportati da AEM Forms:

**JBoss:** org.jnp.interfaces.NamingContextFactory

**WebLogic:** weblogic.jndi.WLInitialContextFactory

**WebSphere:** com.ibm.websphere.naming.WsnInitialContextFactory

**Nome utente di connessione:** nome utente associato alla connessione. Il valore predefinito è guest.

**Password di connessione:** password associata al nome utente specificato in Nome utente della connessione. Il valore predefinito è guest.

**Altre proprietà:** coppie nome proprietà/valore che puoi passare al provider di servizi JNDI. Queste proprietà dipendono dall’implementazione e dalla configurazione del provider in uso.

Le coppie nome proprietà/valore sono separate da punti e virgola **;**. Ad esempio, il testo seguente mostra il valore che verrebbe specificato per due proprietà denominate name1 e name2, con i valori value1 e value2 rispettivamente:

`name1=value1;name2=value2`

## Impostazioni servizio LDAP {#ldap-service-settings}

Il servizio LDAP ( `LDAPService`) fornisce operazioni per l’esecuzione di query sulle directory LDAP. Le directory LDAP vengono in genere utilizzate per memorizzare informazioni sulle persone, i gruppi e i servizi di un’organizzazione.

Per il servizio LDAP sono disponibili le seguenti impostazioni.

**Factory del contesto iniziale:** classe Java da utilizzare come factory del contesto. Questa classe viene utilizzata per creare una connessione al server LDAP. Il valore predefinito è com.sun.jndi.ldap.LdapCtxFactory, che risulta appropriato per la maggior parte dei server LDAP.

**URL del provider:** URL da utilizzare per la connessione al servizio LDAP. Il formato del valore è `ldap://server name:port`

*Nome server* è il nome del computer che ospita il server LDAP

*Porta* è la porta di comunicazione utilizzata dal servizio LDAP. Il valore predefinito è 389, che è la porta standard utilizzata per le connessioni LDAP.

**Nome utente:** nome dell’account utente da utilizzare per accedere al server LDAP. L’account utente deve disporre delle autorizzazioni per connettersi al server e per leggere le informazioni nella directory LDAP.

A seconda del server LDAP, il nome utente potrebbe essere un nome utente semplice come `myname` o un DN come `cn=myname,cn=users,dc=myorg`.

**Password:** la password che corrisponde al nome utente fornito per l’impostazione Nome utente.

**Altre proprietà:** stringa che rappresenta altre proprietà e i valori corrispondenti che puoi fornire al server LDAP. Il valore ha il formato seguente:

`property=value;property=value;...`

## Impostazioni del servizio di configurazione di Microsoft SharePoint {#microsoft-sharepoint-configuration-service-settings}

Il servizio di configurazione di Microsoft SharePoint `(MSSharePointConfigService)` consente di specificare le credenziali per l’utente di AEM Forms con autorizzazioni di rappresentazione. Per informazioni sulle autorizzazioni di rappresentazione, consulta [Configurazione del connettore per Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html).

Per il servizio di configurazione di Microsoft SharePoint sono disponibili le impostazioni seguenti:

* Nome utente per un utente con autorizzazioni di rappresentazione
* Password per l’utente sopra indicato

**Abilita SSL (HTTPS):**

**Durata:** durata in secondi della validità e della memorizzazione nella cache del profilo di provisioning. Il valore predefinito è 86400 (24 ore). Quando un’applicazione client si sincronizza con il server e il tempo specificato è trascorso, l’applicazione client richiede un nuovo profilo di provisioning al server.

**Crittografia:** consente di specificare se crittografare i dati archiviati nel dispositivo mobile.

**Applicazione di Forms:** abilita la funzionalità Moduli nelle applicazioni client per dispositivi mobili. Quando questa opzione è selezionata, gli utenti possono aprire i moduli e avviare i processi dai propri dispositivi mobili.

**Applicazione di Attività:** abilita la funzionalità Attività nelle applicazioni client per dispositivi mobili. Quando questa opzione è selezionata, gli utenti possono accedere ai propri elenchi di attività e completare attività dai propri dispositivi mobili.

**Applicazione di Content Services:** abilita la funzionalità Content Services nell’applicazione client per dispositivi mobili. Questa funzione è disponibile solo per iOS. Quando questa opzione è selezionata, gli utenti di iPhone e iPad possono accedere ai file archiviati nel server WebDAV della tua organizzazione.

**Supporto offline:** consente agli utenti di continuare a utilizzare le applicazioni client per dispositivi mobili anche quando non dispongono di una connessione al server (ad esempio quando non rientrano nell’intervallo di celle o sono in modalità aereo). Gli utenti devono inoltre abilitare l’impostazione Supporto offline sui propri dispositivi mobili. Questa funzione è disponibile per i dispositivi Android e iOS. Per impostazione predefinita, questa funzione è disattivata.

>[!NOTE]
>
>Se il supporto offline è stato abilitato e poi lo disattivi, i profili di provisioning degli utenti vengono aggiornati immediatamente o non appena sono online. Se un utente lavora in modalità offline, tutte le attività in sospeso vengono restituite al relativo elenco Attività e tutti gli elementi nella coda, inclusi i moduli in sospeso, le attività e i moduli contenenti errori di convalida, vengono eliminati dalla coda.

**Android:** consente ai dispositivi Android di connettersi al server.

**Apple iOS:** consente a iPhone e iPad di connettersi al server.

**AIR:** consente ai dispositivi in cui sono in esecuzione app basate su Adobe AIR® di connettersi al server.

**BlackBerry:** consente ai dispositivi BlackBerry di connettersi al server.

**È richiesto Exchange ActiveSync di Microsoft su Android:** specifica se il gestore di criteri di Microsoft Exchange ActiveSync (EAS) deve essere installato e attivo sui dispositivi Android. Quando questa opzione è selezionata, EAS deve essere applicato sul dispositivo Android. Se questa opzione non è selezionata, non viene eseguito alcun controllo, anche se vengono ancora applicati altri requisiti.

**Lunghezza minima del PIN su Android:** i dispositivi Android devono avere un’impostazione globale che impone che il PIN o la password abbia almeno questa lunghezza. Non è sufficiente disporre di un PIN della lunghezza specificata. La lunghezza del PIN deve essere imposta dal sistema in modo che gli utenti non possano rimuoverlo o accorciarlo in un secondo momento. Il valore predefinito è 4.

**Numero massimo di nuovi tentativi di password su Android prima della cancellazione dei dati:** i dispositivi Android hanno un’impostazione globale che cancella il sistema dopo un numero specificato di tentativi di inserimento della password non validi. Questa impostazione globale è abilitata ed è uguale o inferiore al valore specificato qui. Il valore predefinito è 5.

**Cancellazione dei dati su Android alla rimozione:** specifica cosa accade quando si verifica una violazione dei criteri su un dispositivo Android. Quando questa opzione è selezionata, l’account viene eliminato. Se questa opzione non è selezionata, la password dell’account archiviata e i dati memorizzati nella cache vengono eliminati. Non vengono più effettuati tentativi di sincronizzazione finché l’utente non corregge la violazione dei criteri.

## Impostazioni del servizio di output {#output-service-settings}

Il servizio di output `(OutputService)` consente di unire i dati del modulo XML con una progettazione del modulo creata in AEM Forms Designer per creare un flusso di output di documenti in uno dei seguenti formati:

* Flusso di output di un documento PDF o PDF/A.
* Flusso di output di Adobe PostScript.
* Flusso di output di PCL (Printer Control Language).
* Flusso di output di Zebra Programming Language (ZPL).

Il flusso di output può essere inviato a una stampante di rete, a una stampante locale o a un file su disco. Quando utilizzi il servizio di output come parte di un processo, puoi anche inviare il flusso di output a un destinatario e-mail come allegato di un file.

Per il servizio output sono disponibili le seguenti impostazioni.

**Tipo di transazione:** specifica la modalità di propagazione di un contesto di transazione a un’operazione:

**Obbligatorio:** supporta un contesto di transazione se ne esiste già uno; in caso contrario, viene creato un nuovo contesto di transazione. Questo è il valore predefinito.

**Nuovo obbligatorio:** crea sempre un nuovo contesto di transazione. Se esiste un contesto di transazione attivo, viene sospeso.

**Timeout transazione (in sec):** il numero di secondi di attesa del provider di transazioni sottostante prima del rollback di una transazione che esegue il wrapping di questa operazione. Questo valore viene ignorato se viene propagato un contesto di transazione esistente.

Quando elabori file di dati di grandi dimensioni o lavori su un server occupato, potrebbe essere necessario aumentare il timeout del servizio di output. Per modificare il valore di timeout, verifica che i server hardware dispongano di memoria adeguata e che la memoria sia disponibile per l’heap del server applicazioni Java. Il valore predefinito è `180`.

## Impostazioni del servizio di configurazione PDFG {#pdfg-config-service-settings}

Le impostazioni seguenti sono disponibili per il servizio di configurazione PDFG ( `PDFGConfigService`).

**Directory opzioni del processo utente:** il percorso della cartella del file system in cui il servizio c scrive i file delle opzioni del processo accessibili ad Acrobat Pro Extended. Il valore predefinito è [user.home]/Application Data/Adobe/Adobe PDF/Settings.

**Directory di avvio PS:** il percorso della cartella del file system in cui vengono salvati i file di avvio richiesti da Adobe Acrobat Distiller. Il valore predefinito è [user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup.

**File di avvio PS:** il nome del file di avvio richiesto da Adobe Acrobat Distiller. Il valore predefinito è example.ps.

**Timeout conversione server:** il timeout massimo di conversione del processo (in secondi) per il servizio di generazione PDF e il servizio Distiller. Questa impostazione limita il timeout massimo di conversione che puoi specificare nel file config.xml e nelle pagine della console di amministrazione per PDF Generator. Il valore predefinito è 270.

**Timeout globale del server:** durante l’esecuzione delle conversioni di PDF, un server Forms tiene conto del limite di timeout. Per risolvere il problema, configura il valore di timeout.

**Prefisso opzioni processo:** il prefisso utilizzato dal servizio di generazione PDF per anteporre una breve stringa ai file delle opzioni processo creati temporaneamente per l’utilizzo da parte di Acrobat Distiller. Il valore predefinito è pdfg.

**App non Unicode:** un elenco separato da virgole di nomi di applicazioni che non supportano Unicode. Questo elenco è precompilato con i nomi di diverse applicazioni, il cui supporto è preconfigurato in PDF Generator. Se scegli di aggiungere il supporto per le conversioni PDF tramite altre applicazioni di terze parti che non supportano Unicode, devi aggiungerle a questo elenco. Il valore predefinito è Autocad,Excel,PowerPoint,Project,Publisher,Visio,Word,WordPerfect.

**Conteggio pool thread del server:** controlla le dimensioni del pool di thread utilizzato internamente dal servizio di generazione PDF per soddisfare le richieste di conversione da HTML a PDF che implicano spider (conversione di pagine collegate accessibili dalla pagina principale). Il valore predefinito è 20.

**Scansione di pulizia PDFG in secondi:** per ulteriori dettagli, consulta la sezione Scadenze processo in secondi.

**Scadenza processo in secondi:** il servizio di generazione PDF elimina i file di input non appena vengono convertiti. Memorizza temporaneamente i file di output, per un periodo di tempo determinato dalle impostazioni Scansione di pulizia PDFG in secondi e Scadenza processo in secondi.

L’impostazione Scadenza processo in secondi specifica l’età di un file o di una cartella vuota prima che sia possibile eliminarlo. L’impostazione Scansione di pulizia PDFG in secondi specifica la frequenza con cui un thread di pulizia esegue la scansione delle cartelle temporanee per individuare i file che possono essere eliminati.

Ad esempio, se Scadenza processo in secondi è impostata su 100 e Scansione di pulizia PDFG in secondi è impostata su 200, il thread di pulizia viene eseguito ogni 200 secondi ed elimina i file di almeno 100 secondi.

Il valore predefinito di Scansione di pulizia PDFG in secondi è `43200` (12 ore). Il valore predefinito per Scadenza processo in secondi è `86400` (24 ore).

**Lingua predefinita:** consente di ignorare la lingua predefinita (paese + lingua) del server in cui è distribuito il servizio di generazione PDF. Se questo parametro non è specificato, la lingua predefinita viene determinata in base al sistema operativo in cui il servizio viene distribuito. Questo parametro controlla la lingua in cui i messaggi di errore vengono restituiti alle API.

## Impostazioni del servizio Servizi dati Forms Workflow {#forms-workflow-data-services-service-settings}

I servizi seguenti estendono i servizi dati ed espongono gli assembler utilizzati da Workspace per comunicare con il server. Non modificare le opzioni di configurazione per questi servizi a meno che non ricevi istruzioni in tal senso dal supporto Adobe. Questi servizi non sono destinati all’accesso diretto:

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## Impostazioni del servizio di comunicazione remota {#remoting-service-settings}

La maggior parte dei servizi è configurata in modo da potervi accedere tramite AEM Forms Remoting (obsoleto per AEM Forms). Per informazioni su AEM Forms Remoting (obsoleto per AEM Forms), consulta [Programmazione con AEM Forms](https://adobe.com/go/learn_aemforms_programming_63).

Per il servizio di remoting sono disponibili le impostazioni seguenti.

**Metodo di autenticazione client Flex:** determina il tipo di risposta che il server invia al client quando il servizio richiamato è abilitato per la protezione, l’operazione richiamata non supporta chiamate anonime e il client non trasmette credenziali o le trasmette non valide. Puoi scegliere tra Personalizzato o Base. Il valore predefinito è Base.

**Consenti la serializzazione di classi non serializzabili:** la maggior parte degli endpoint di AEM Forms consente di utilizzare solo classi serializzabili per la chiamata. Nelle versioni precedenti, l’endpoint di remoting consentiva l’utilizzo di classi non serializzabili per le chiamate dai client basati su Flex. Per evitare una vulnerabilità di sicurezza descritta in APS11-15, questa impostazione è stata modificata. Se vuoi continuare a utilizzare le classi non serializzabili con l’endpoint servizio di remoting Flex, seleziona questa casella di controllo.

## Impostazioni del servizio dell’archivio {#repository-service-settings}

Il servizio dell’archivio ( `RepositoryService`) fornisce servizi di archiviazione e gestione delle risorse per AEM Forms. Quando gli sviluppatori creano un’applicazione, possono distribuire le risorse nell’archivio anziché in un file system. Le risorse possono includere qualsiasi tipo di materiale collaterale, tra cui moduli XML, moduli PDF (inclusi i moduli Acrobat), frammenti di modulo, immagini, profili, criteri, file SWF, file DDX, schemi XML, file WSDL e dati di test.

Puoi utilizzare l’archivio predefinito incluso in AEM Forms oppure un archivio di terze parti (EMC Documentum Content Server, IBM FileNet Content Manager o IBM Content Manager).

Il servizio del provider dell’archivio è un delegato del servizio che funge da interfaccia per un servizio del provider. Questo ti consente di connetterti a un’API comune e di non dover sapere quale servizio del provider sta implementando le funzionalità di archiviazione. Il servizio Provider dell’archivio fornisce l’archiviazione del database per le risorse del servizio di archivio.

Per il servizio di archivio è disponibile la seguente impostazione.

**Servizio del provider:** il nome del servizio utilizzato come provider di archiviazione. Il valore predefinito è RepositoryProviderService.

## Impostazioni servizio di firma {#signature-service-settings}

Il servizio di firma ( `SignatureService`) consente all’organizzazione di garantire la protezione e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza le firme digitali e la certificazione per garantire che i documenti non vengano modificati. La modifica di un documento ne interrompe la firma. Poiché le funzioni di protezione vengono applicate al documento stesso, il documento rimane protetto e controllato per l’intero ciclo di vita, oltre il firewall, quando viene scaricato offline e quando viene inviato nuovamente all’organizzazione.

Per il servizio di firma sono disponibili le impostazioni seguenti.

**Nome del servizio SPI HSM remoto:** questa opzione va utilizzata quando HSM è installato in un computer remoto. Specifica questa opzione quando AEM Forms è installato in un ambiente Windows a 64 bit e utilizzi dispositivi HSM per la firma.

**URL del servizio web HSM remoto:** specifica questa opzione quando AEM Forms è installato su Windows a 64 bit e utilizzi dispositivi HSM per la firma.

**Certificazione per includere le modifiche al caricamento del modulo:** quando questa opzione è selezionata, oltre al modello XFA viene certificato lo stato del modulo XFA. L’abilitazione di questa opzione può influire negativamente sulle prestazioni. Il valore predefinito è vero.

**Esegui gli script JavaScript del documento:** specifica se eseguire script documento JavaScript durante le operazioni di firma. Il valore predefinito è falso.

**Elabora documenti con compatibilità Acrobat 9:** specifica se abilitare la compatibilità con Acrobat 9. Ad esempio, quando questa opzione è selezionata, Certificazione visibile nei PDF dinamici è abilitata. Il valore predefinito è falso.

**Includi le informazioni di revoca durante la firma:** specifica se le informazioni di revoca vengono incluse durante la firma del documento PDF. Il valore predefinito è falso.

**Includi le informazioni di revoca durante la certificazione:** specifica se le informazioni di revoca vengono incorporate durante la certificazione del documento PDF. Il valore predefinito è falso.

**Applica l’inclusione delle informazioni di revoca per tutti i certificati durante la firma/certificazione:** specifica se un’operazione di firma o certificazione non riesce quando non sono incorporate informazioni di revoca valide per tutti i certificati. Si noti che se un certificato non contiene informazioni CRL o OCSP, viene considerato valido anche se non vengono recuperate informazioni di revoca. Il valore predefinito è falso.

**Ordine di verifica della revoca:** specifica l’ordine di verifica della revoca quando la verifica è possibile tramite i meccanismi CRL (Certificate Revocation List) e OCSP (Online Certificate Status Protocol). Il valore predefinito è OCSPFirst.

**Dimensione massima delle informazioni archiviate sulla revoca:** la dimensione massima delle informazioni archiviate sulla revoca in kilobyte. AEM Forms tenta di memorizzare il volume massimo possibile di informazioni della revoca senza superare il limite. Il valore predefinito è 10 KB.

**Supporta le firme create con versioni pre-release dei prodotti Adobe:** quando questa opzione è selezionata, la firma creata con una versione prerelease dei prodotti Adobe verrà convalidata correttamente. Il valore predefinito è falso.

**Opzione per il tempo di verifica:** specifica il tempo della verifica del certificato di un firmatario. Il valore predefinito è Ora protetta diversa dall’ora corrente.

**Utilizza le informazioni di revoca archiviate nella firma durante
la convalida:** specifica se le informazioni di revoca archiviate con la firma vengono utilizzate per il controllo della revoca. Il valore predefinito è vero.

**Utilizza le informazioni di convalida archiviate nel documento per
la convalida delle firme:** quando questa opzione è selezionata, per convalidare le firme vengono utilizzate le informazioni di convalida (incluse le informazioni di revoca e marca temporale) incorporate nel documento. Il valore predefinito è vero.

**Numero massimo di sessioni di verifica nidificate consentite:** numero massimo di sessioni di verifica nidificate consentite. AEM Forms utilizza questo valore per evitare un ciclo infinito durante la verifica dei certificati del firmatario OCSP o CRL quando quest’ultimo non è configurato correttamente. Il valore predefinito è 10.

**Deviazione massima dell’orario per la verifica:** tempo massimo, in minuti, per la firma dopo il tempo di convalida. Se la deviazione dell’orario è maggiore di questo valore, la firma non sarà valida. Il valore predefinito è di 65 minuti.

**Cache della durata del certificato:** la durata di un certificato, recuperato online o tramite altri mezzi, nella cache. Il valore predefinito è 1 giorno.

### Opzioni di trasporto {#transport-options}

**Host proxy:** URL dell’host proxy. Utilizzato solo se viene fornito un valore valido. Nessun valore predefinito.

**Porta proxy:** porta proxy. Digita un numero di porta valido compreso tra 0 e 65535. Il valore predefinito è 80.

**Nome utente per l’accesso al proxy:** nome utente per l’accesso al proxy. Utilizzato solo se viene fornito un valore valido per l’host proxy e la porta proxy. Nessun valore predefinito.

**Password per l’accesso al proxy:** password per l’accesso al proxy. Utilizzato solo se viene fornito un valore valido per l’host proxy, la porta proxy e il nome utente per l’accesso al proxy. Nessun valore predefinito.

**Limite massimo di download:** quantità massima di dati, in MB, che può essere ricevuta per connessione. Il valore minimo è 1 MB e quello massimo è 1024 MB. Il valore predefinito è 16 MB.

**Timeout di connessione:** tempo massimo di attesa, in secondi, per stabilire una nuova connessione. Il valore minimo è 1 e quello massimo è 300. Il valore predefinito è 5.

**Timeout del socket:** tempo massimo di attesa, in secondi, prima del timeout del socket (durante l’attesa del trasferimento dei dati). Il valore minimo è 1 e quello massimo è 3600. Il valore predefinito è 30.

### Opzioni di convalida del percorso {#path-validation-options}

**Richiedi criterio esplicito:** specifica se il percorso deve essere valido per almeno uno dei criteri dei certificati associato all’ancoraggio di affidabilità del certificato del firmatario. Il valore predefinito è falso.

**Inibisci QUALSIASI criterio:** specifica se l’identificatore dell’oggetto dei criteri (OID) deve essere elaborato se è incluso in un certificato. Il valore predefinito è falso.

**Inibisci mappatura criteri:** specifica se la mappatura dei criteri è consentita nel percorso di certificazione. Il valore predefinito è falso.

**Controlla tutti i percorsi:** specifica se tutti i percorsi devono essere convalidati o se la convalida deve essere interrotta dopo aver trovato il primo percorso valido. Seleziona vero o falso. Il valore predefinito è falso.

**Server LDAP:** server LDAP utilizzato per cercare i certificati per la convalida del percorso. Nessun valore predefinito.

**Segui URI in certificato AIA:** specifica se gli Identificatori di risorse uniformi (URI) in certificato AIA vengono elaborati durante l’individuazione del percorso. Il valore predefinito è falso.

**Estensione dei vincoli di base richiesta nei certificati CA:** specifica se l’estensione del certificato dei vincoli di base dell’autorità di certificazione (CA) deve essere presente per i certificati CA. Alcuni certificati radice tedeschi meno recenti (7 e precedenti) non sono conformi alla RFC 3280 e non contengono l’estensione del vincolo di base. Se sai che il certificato EE di un utente è concatenato fino a una certificato radice tedesco di questo tipo, deseleziona questa casella di controllo. Il valore predefinito è vero.

**Richiedi una firma del certificato valida durante la creazione della catena:** specifica se il generatore di catene richiede firme valide nei certificati utilizzati per la creazione delle catene. Quando questa casella di controllo è selezionata, il generatore di catene non crea catene con firme RSA non valide nei certificati. Considera la catena CA > ICA > EE se la firma della CA su un ICA non è valida. Se questa impostazione è vera, la costruzione della catena si fermerà all’ICA e la CA non verrà inclusa nella catena. Se questa impostazione è falsa, viene prodotta la catena completa di 3 certificati. Questa impostazione non influisce sulle firme DSA. Il valore predefinito è falso.

### Opzioni del provider di timestamp {#timestamp-provider-options}

**URL del server TSP:** URL del provider di timestamp predefinito. Utilizzato solo se viene fornito un valore valido. Nessun valore predefinito.

**Nome utente server TSP:** nome utente, se richiesto dal provider di timestamp. Utilizzato solo se viene fornito un valore valido per l’URL. Nessun valore predefinito.

**Password del server TSP:** password per il nome utente indicato, se richiesta dal provider di timestamp. Utilizzata solo se vengono forniti valori validi per l’URL e il nome utente. Nessun valore predefinito.

**Algoritmo di hash della richiesta:** specifica l’algoritmo di hash da utilizzare durante la creazione della richiesta per il provider di timestamp. Il valore predefinito è SHA1.

**Stile di verifica della revoca:** specifica lo stile di verifica della revoca utilizzato per determinare lo stato di attendibilità del certificato del provider del timestamp, in base allo stato di revoca osservato. Il valore predefinito è BestEffort.

**Invia Nonce:** specifica se viene inviato un Nonce con la richiesta del provider timestamp. Un nonce può essere una marca temporale, un contatore di visite su una pagina web o un marcatore speciale che ha lo scopo di limitare o impedire la ripetizione o la riproduzione non autorizzate di un file. Il valore predefinito è vero.

**Usa marche temporali scadute durante la convalida:** se questa opzione è selezionata, è possibile utilizzare marche temporali scadute per recuperare i tempi di convalida delle firme. Il valore predefinito è vero.

**Dimensione della risposta TSP:** dimensione in byte stimata della risposta TSP. Questo valore rappresenta la dimensione massima della risposta del timestamp che il provider del timestamp configurato può restituire. Non modificare questa impostazione se non hai la certezza assoluta. Il valore minimo è 60 B e il valore massimo è 10240 B. Il valore predefinito è 4096 B.

**Ignora estensione del server di marca temporale**: seleziona l’opzione **Ignora estensione del server marca temporale** per impedire al server AEM Forms di contattare il server della marca temporale specificato. La selezione di questa opzione consente di evitare errori di processo che si verificano a causa del timeout di connessione tra i server di AEM Forms e della marca temporale.

### Opzioni dell’elenco di revoca di certificati {#certificate-revocation-list-options}

**Consulta prima l’URI locale:** specifica se la posizione CRL specificata nell’URI locale o nella ricerca CRL deve avere la preferenza rispetto a qualsiasi posizione specificata in un certificato ai fini della verifica delle revoche. Il valore predefinito è falso.

**URI locale per la ricerca della CRL:** URL del provider CRL locale. Questo valore viene consultato solo se l’opzione Consulta in primo luogo l’URI locale è impostata su vero. Nessun valore predefinito.

**Stile di verifica della revoca:** specifica lo stile di verifica della revoca utilizzato per determinare lo stato di attendibilità del certificato del provider CRL inbase allo stato di revoca osservato. Il valore predefinito è BestEffort.

**Server LDAP la per ricerca della CRL:** server LDAP utilizzato per ottenere i CRL (come www.ldap.com). Tutte le query basate su DN per i CRL verranno indirizzate a questo server. Nessun valore predefinito.

**Passare online:** specifica se passare online per recuperare un CRL. Se l’impostazione è falso, vengono consultati solo i CRL memorizzati nella cache (sul disco locale o incorporati con la firma). Il valore predefinito è vero.

**Ignora date validità:** specifica se ignorare i tempi thisUpdate e nextUpdate di risposta, che impediscono a questi tempi di avere un effetto negativo sulla validità della risposta. Il valore predefinito è falso.

**Richiedi estensione AKI nel CRL:** specifica se l’estensione Identificatore della chiave dell’autorità (AKI) deve essere inclusa in un CRL. Il valore predefinito è falso.

### Opzioni del protocollo di stato del certificato in linea {#online-certificate-status-protocol-options}

**URL del server OCSP:** URL del server OCSP predefinito. L’utilizzo del server OCSP specificato tramite questo URL dipende dall’impostazione dell’opzione URL da consultare. Nessun valore predefinito.

**Opzione URL da consultare:** controlla l’elenco e l’ordine dei server OCSP utilizzati per eseguire il controllo dello stato. Il valore predefinito è UseAIAInCert.

**Stile controllo revoca:** specifica lo stile del controllo della revoca utilizzato durante la verifica del certificato del server OCSP. Il valore predefinito è CheckIfAvailable.

**Invia Nonce:** specifica se un nonce viene inviato con la richiesta OCSP. Un nonce può essere una marca temporale, un contatore di visite su una pagina web o un marcatore speciale che ha lo scopo di limitare o impedire la ripetizione o la riproduzione non autorizzate di un file. Il valore predefinito è vero.

**Tempo deviazione massima orario:** deviazione massima consentita, in minuti, tra il tempo di risposta e l’ora locale. Il valore minimo è 0 e il valore massimo è 2147483647 m. Il valore predefinito è 5m.

**Ora di aggiornamento risposta:** tempo massimo, in minuti, per il quale una risposta OCSP precostruita è considerata valida. Il valore minimo è 1m e il valore massimo consentito è 2147483647. Il valore predefinito è 525600 (un anno).

**Firma delle richiesta OCSP:** specifica se la richiesta OCSP deve essere firmata. Il valore predefinito è falso.

**Alias credenziali firmatario richiesta:** specifica l’alias delle credenziali da utilizzare per la firma della richiesta OCSP se la firma è abilitata. Utilizzato solo se la firma della richiesta OCSP è abilitata. Nessun valore predefinito.

**Vai online:** specifica se andare online per eseguire il controllo della revoca. Il valore predefinito è vero.

**Ignora i tempi thisUpdate e nextUpdate di risposta:** specifica se ignorare i tempi thisUpdate e nextUpdate di risposta, che impedisce a questi tempi di avere un effetto negativo sulla validità della risposta. Il valore predefinito è falso.

**Consenti estensione OCSPNoCheck:** specifica se l’estensione OCSPNoCheck è consentita nel certificato di firma della risposta. Il valore predefinito è vero.

**Richiedi estensione CertHash OCSP ISIS-MTT:** specifica se nelle risposte OCSP deve essere inclusa un’estensione hash della chiave pubblica del certificato. Il valore predefinito è falso.

### Opzioni di gestione degli errori per il debug {#error-handling-options-for-debugging}

**Elimina cache certificati nella chiamata API successiva:** specifica se eliminare la cache certificati quando viene richiamata l’operazione successiva del servizio di firma. Una volta richiamata l’operazione, questa opzione viene impostata nuovamente su falso. Il valore predefinito è falso.

**Elimina cache CRL nella chiamata API successiva:** specifica se eliminare la cache CRL quando viene richiamata l’operazione successiva del servizio di firma. Una volta richiamata l’operazione, questa opzione viene impostata nuovamente su falso. Il valore predefinito è falso.

**Elimina cache OCSP nella chiamata API successiva:** specifica se eliminare la cache OCSP quando viene richiamata l’operazione successiva del servizio di firma. Una volta richiamata l’operazione, questa opzione viene impostata nuovamente su falso. Il valore predefinito è falso.

## Impostazioni servizio cartella controllata {#watched-folder-service-settings}

Il servizio Cartella controllata ( `WatchedFolder`) configura gli attributi comuni a tutti gli endpoint della cartella controllata. Fornisce inoltre valori predefiniti per gli endpoint della cartella controllata. (Consulta [Configurazione degli endpoint della cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).) Non viene richiamata da applicazioni client esterne o utilizzata nei processi creati in Workbench.

Per il servizio Cartella controllata sono disponibili le impostazioni seguenti.

**Espressione cron:** espressione cron come quella utilizzata da Quartz per pianificare il polling della directory di input.

**Conteggio ripetizioni:** il numero di volte in cui viene eseguito il polling della directory di input. Il conteggio delle ripetizioni predefinito da utilizzare se questo valore non è specificato nella configurazione dell’endpoint. Il valore -1 indica l’analisi indefinita della directory. Il valore predefinito è -1.

**Intervallo di ripetizione:** il numero predefinito in secondi tra ciascun sondaggio. Questo valore viene utilizzato come intervallo di ripetizione a meno che non venga specificato un valore diverso nella configurazione dell’endpoint della cartella esaminata. Il valore predefinito è 5. Per ulteriori informazioni, consulta la descrizione dell’impostazione Dimensione batch.

**Asincrono:** identifica il tipo di chiamata come asincrono o sincrono. I processi transitori e sincroni possono essere richiamati solo in modo sincrono. Il valore predefinito è asincrono.

**Tempo di attesa:** valore predefinito espresso in secondi dopo il quale i file vengono recuperati dalle cartelle di input. Se il file o la cartella è precedente al tempo di attesa specificato, viene prelevato per l’elaborazione. Il valore predefinito è 0.

**Dimensione batch:** valore predefinito per il numero di file o cartelle elaborati per la scansione. Il valore predefinito è 2.

Le impostazioni Intervallo di ripetizione e Dimensione batch determinano il numero di file che la cartella esaminata può raccogliere in ogni analisi. La cartella esaminata utilizza un pool di thread Quartz per analizzare la cartella di input. Il pool di thread è condiviso con altri servizi. Se l’intervallo di scansione è ridotto, i thread eseguono spesso la scansione della cartella di input. Se i file vengono rilasciati frequentemente nella cartella esaminata, mantieni l’intervallo di scansione ridotto. Se i file vengono eliminati raramente, utilizza un intervallo di scansione più ampio in modo che gli altri servizi possano utilizzare i thread.

Se elimini un grande volume di file, ingrandisci la dimensione del batch. Ad esempio, se il servizio richiamato dall’endpoint della cartella esaminata è in grado di elaborare 700 file al minuto e gli utenti rilasciano i file nella cartella di input alla stessa velocità, impostare Dimensione batch su 350 e Intervallo di ripetizione su 30 secondi migliorerà le prestazioni della cartella controllata senza incorrere troppo nel costo della scansione della stessa.

Quando i file vengono rilasciati nella cartella controllata, vengono elencati i file nell’input, il che può ridurre le prestazioni se la scansione viene eseguita ogni secondo. L’aumento dell’intervallo di scansione può migliorare le prestazioni. Se il volume dei file da eliminare è piccolo, regola di conseguenza le dimensioni del batch e l’intervallo di ripetizione. Ad esempio, se vengono rilasciati 10 file al secondo, prova a impostare Intervallo di ripetizione su 1 secondo e Dimensione batch su 10.

In una configurazione cluster, la dimensione batch per un endpoint di cartella controllata non viene scalata in più nodi cluster. Ad esempio, se la dimensione batch è impostata su `2` per un cluster a due nodi e l’opzione Limitazione è selezionata, i nodi elaborano i file collettivamente in batch di due invece che elaborare singolarmente due file alla volta.

**Sovrascrivi nomi di file duplicati:** stringa booleana che specifica se i nomi di file dei risultati duplicati vengono sovrascritti dalla cartella controllata e se i documenti conservati con lo stesso nome devono essere sovrascritti.

**Mantieni cartella:** il valore predefinito per la cartella. Questa cartella viene utilizzata per copiare i file di origine in caso di elaborazione corretta dell’input. Questo valore può essere un percorso vuoto, relativo o assoluto con un modello di file come descritto per l’impostazione Cartella risultati.

**Cartella errori:** il nome della cartella in cui vengono copiati i file con gli errori. Questo valore può essere un percorso vuoto, relativo o assoluto con un modello di file come descritto per l’impostazione Cartella risultati.

**Cartella risultati:** il nome predefinito per la cartella dei risultati. Questa è la cartella in cui vengono copiati i file con i risultati. Questo valore può essere un percorso vuoto, relativo o assoluto con il seguente pattern di file.

* %F = prefisso del nome file
* %E = estensione del nome file
* %Y = anno (completo)
* %y = anno (ultime due cifre)
* %M = mese
* %D = giorno del mese
* %d = giorno dell’anno
* %H = ora (24 ore)
* %h = ora (12 ore)
* %m = minuto
* %s = secondo
* %l = millisecondo
* %R = numero casuale da 0 a 9
* %P = ID processo

Ad esempio, se sono le 20:00 del 17 luglio 2009 e specifichi `C:/Test/WF0/failure/%Y/%M/%D/%H/`, la cartella dei risultati sarà `C:/Test/WF0/failure/2009/07/17/20`.

Se il percorso non è assoluto ma relativo, la cartella viene creata all’interno della cartella controllata. Per ulteriori informazioni sui modelli di file, consulta [Informazioni sui pattern di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Minore è la dimensione delle cartelle dei risultati, migliori saranno le prestazioni della cartella controllata. Ad esempio, se il carico stimato per la cartella controllata è di 1000 file l’ora, prova un pattern come `result/%Y%M%D%H` in modo che venga creata una nuova sottocartella ogni ora. Se il carico è più piccolo (ad esempio, 1000 file al giorno), puoi utilizzare un pattern come `result/%Y%M%D`.

**Cartella di fase:** nome predefinito per la cartella di fase all’interno della cartella controllata.

**Cartella di input:** nome predefinito per la cartella di input all’interno della cartella controllata.

**Mantieni in caso di errore:** se è impostata su vero, in caso di errore i file originali vengono conservati nella cartella degli errori.

**Limitazione:** quando questa opzione è selezionata, limita il numero di processi delle cartelle controllate che AEM Forms elabora in un momento dato. Il valore Dimensione batch determina il numero massimo di processi. Consulta Informazioni sulla limitazione.

## Impostazioni del servizio Servizio web {#web-service-service-settings}

Il servizio Servizio web ( `WebService`) consente ai processi di richiamare le operazioni del servizio web.

Il servizio Servizio web consente ai processi di richiamare le operazioni del servizio Web. Ad esempio, un’organizzazione potrebbe voler integrare un processo per memorizzare e recuperare informazioni quali i dettagli di contatti e account richiamando i servizi web messi a disposizione da un fornitore di servizi. Il servizio Servizio web richiama un servizio web specificato e trasmette i valori corrispondenti a ciascuno dei relativi parametri. Quindi salva i valori restituiti dall’operazione in una variabile designata all’interno di un processo.

Il servizio Servizio Web interagisce con i servizi web inviando e ricevendo messaggi SOAP. Il servizio supporta inoltre l’invio di allegati MIME, MTOM e SwaRef con i messaggi SOAP tramite il protocollo WS-Attachment. Le interazioni del servizio Servizio web sono compatibili con i sistemi SAP e i servizi web .NET.

Per il servizio Servizio Web sono disponibili le impostazioni seguenti.

**Archivio chiavi:** percorso completo del file dell’archivio chiavi contenente la chiave privata da utilizzare per l’autenticazione. Il server Forms deve essere in grado di accedere al file.

**Password archivio chiavi:** la password per il file dell’archivio chiavi.

**Tipo di archivio chiavi:** Il tipo di archivio chiavi. Non specificare alcun valore per utilizzare il tipo di archivio chiavi predefinito configurato per la JVM che esegue il server Forms. In alternativa, specifica uno dei seguenti valori:

* jks
* pkcs12
* cms
* jceks

**Archivio fonti attendibili:** percorso completo del file dell’archivio fonti attendibili contenente la chiave pubblica del server del servizio web.

**Password archivio fonti attendibili:** password per il file dell’archivio fonti attendibili.

**Tipo di archivio fonti attendibili:** tipo dell’archivio fonti attendibili. Non specificare alcun valore per utilizzare il tipo di archivio chiavi predefinito configurato per la JVM che esegue il server Forms. In alternativa, specifica uno dei seguenti valori:

* jks
* pkcs12
* cms
* jceks

## Impostazioni del servizio di trasformazione XSLT {#xslt-transformation-service-settings}

Il servizio di trasformazione XSLT ( `XSLTService`) consente ai processi di applicare trasformazioni XSLT (Extensible Stylesheet Language Transformations) ai documenti XML.

Per il servizio di trasformazione XSLT è disponibile l’impostazione seguente.

**Nome della factory:** nome completo della classe Java da utilizzare per l’esecuzione delle trasformazioni XSLT. Se non è specificato alcun valore, viene utilizzata la factory predefinita configurata nella Java Virtual Machine che esegue il server Forms.

## Modificare le impostazioni di protezione per un servizio {#modifying-security-settings-for-a-service}

Il server Forms consente di configurare le impostazioni di protezione per ogni servizio, permettendoti di configurare un controllo degli accessi dettagliato a livello di servizio.

Vengono installati i profili di sicurezza predefiniti, che possono essere configurati per soddisfare le esigenze del sistema. A ciascun profilo di sicurezza è associato un dominio e viene creato a livello di utente o di gruppo.

### Modificare le impostazioni di protezione per un servizio {#modify-security-settings-for-a-service}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizio fai clic sul servizio da configurare.
1. Fai clic sulla scheda Protezione.
1. Nell’elenco Richiedi chiamanti da autenticare seleziona Sì o No per specificare se il servizio può essere richiamato con o senza credenziali.

   Se selezioni Sì, il chiamante del servizio deve essere autenticato e l’entità utente principale per quel chiamante deve essere autorizzata a richiamare il servizio. In caso contrario, il tentativo di chiamata verrà rifiutato.

   Se selezioni No, il chiamante del servizio potrebbe essere autenticato o meno. La chiamata del servizio avrà sempre esito positivo perché non è presente alcun controllo di autorizzazione.

1. Per i servizi che contengono una o più operazioni contrassegnate per l’accesso anonimo, seleziona o deseleziona Accesso anonimo consentito. Quando è abilitato l’accesso anonimo, qualsiasi utente all’interno del sistema può richiamare le operazioni sul servizio. Se l’accesso anonimo è disabilitato, agli utenti deve essere concessa l’autorizzazione per chiamare il servizio e richiamare le operazioni. Queste autorizzazioni vengono concesse agli utenti direttamente o in qualità di membri di un gruppo con tali autorizzazioni.
1. Per alcuni servizi, l’account utente che esegue l’operazione influisce sui risultati. Ad esempio, in Content Services (obsoleto), l’utente che memorizza il contenuto diventa il proprietario del contenuto, il che influisce su chi può successivamente accedere al contenuto. Se utilizzi un processo per archiviare il contenuto, dovresti considerare quale utente viene utilizzato per eseguire il servizio di gestione dei documenti, in quanto l’utente sarà proprietario del contenuto memorizzato.

   Per specificare l’identità di runtime utilizzata da un servizio per eseguire operazioni, seleziona Specifica esegui come, seleziona un’opzione dall’elenco associato e quindi fai clic su Salva. Scegli una delle seguenti opzioni:

   **Invoker:** utilizza la stessa identità dell’utente che ha richiamato il servizio.

   **Sistema:** utilizza l’utente di sistema per eseguire il servizio con privilegi completi.

   **Utente con nome:** ti consente di eseguire il servizio come utente specifico. Quando selezioni questa opzione, fai clic su Seleziona utente per visualizzare la pagina Seleziona entità principale, in cui è possibile cercare e selezionare l’utente.

   Se non selezioni Specifica esegui come, viene utilizzato il comportamento predefinito.

   >[!NOTE]
   >
   >I servizi di rendering e invio utilizzati con xfaForm, Document Form e variabili Form vengono sempre eseguiti utilizzando l’account utente di sistema.

1. Fai clic su Aggiungi entità principale per specificare le autorizzazioni di utenti e gruppi per questo servizio.
1. Nella schermata Seleziona entità principale vengono visualizzati gli utenti e i gruppi configurati in Gestione utente. Se l’utente o il gruppo desiderato non viene visualizzato, utilizza la funzione di ricerca per trovarlo. Fai clic sul nome di un utente o un gruppo.
1. Nella schermata Aggiungi autorizzazioni, seleziona le autorizzazioni da assegnare all’utente o al gruppo per questo servizio:

   * **INVOKE_PERM:** per richiamare tutte le operazioni nel servizio
   * **MODIFY_CONFIG_PERM:** per modificare la configurazione di un servizio
   * **SUPERVISOR_PERM:** per visualizzare i dati dell’istanza di processo per un servizio creato da un processo
   * **START_STOP_PERM:** per avviare e arrestare un servizio
   * **ADD_REMOVE_ENDPOINTS_PERM:** per aggiungere, rimuovere e modificare endpoint per un servizio
   * **CREATE_VERSION_PERM:** per creare una versione del servizio
   * **DELETE_VERSION_PERM:** per eliminare una versione del servizio
   * **MODIFY_VERSION_PERM:** per modificare una versione del servizio
   * **READ_PERM:** per visualizzare il servizio
   * **PROCESS_OWNER_PERM:** da usare in una versione futura di AEM Forms. Non utilizzare questa autorizzazione.
   * **SERVICE_MANAGER_PERM:** da utilizzare in una versione futura di AEM Forms. Non utilizzare questa autorizzazione.
   * **SERVICE_AGENT_PERM:** da utilizzare in una versione futura di AEM Forms. Non utilizzare questa autorizzazione.

1. Fai clic su Aggiungi.

### Rimuovere l’entità principale da un profilo di sicurezza {#remove-the-principal-from-a-security-profile}

1. Nella pagina Gestione servizio, seleziona il servizio da configurare.
1. Fai clic sulla scheda **Protezione**, seleziona il profilo di protezione da rimuovere, quindi fai clic su **Rimuovi**.

## Configurare il pooling per un servizio {#configuring-pooling-for-a-service}

Ogni servizio può sfruttare le funzionalità di pooling per gestire le richieste di chiamata in ingresso. L’utilizzo di un pool di servizi garantisce che le istanze del servizio vengano richiamate da un singolo thread alla volta e riutilizzate in più richieste di chiamata, con conseguente miglioramento delle prestazioni. Puoi inoltre utilizzare il pooling per specificare l’opzione Numero massimo di istanze del servizio asincrono, che consente ai servizi di limitare il numero di richieste gestite in parallelo.

### Abilitare il pooling {#enable-pooling}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizio fai clic sul servizio da configurare.
1. Fai clic sulla scheda Pooling.
1. Nell’elenco Strategia di elaborazione delle richieste seleziona Istanze in pool per Tutte le richieste.
1. Nella casella Dimensione iniziale del pool di istanze del servizio immetti la dimensione iniziale del pool. Quando il servizio viene distribuito, questo valore viene utilizzato per determinare il numero di istanze di implementazione del servizio create e allocate al pool libero, in attesa di richieste di chiamata. In questo modo il contenitore del servizio può rispondere immediatamente alle richieste di chiamata senza dover prima inizializzare un’istanza del servizio.
1. Nella casella Dimensione massima del pool di istanze del servizio immetti il numero massimo di istanze presenti nel pool per un determinato servizio. Questa impostazione controlla il numero di thread che possono eseguire un determinato servizio in un momento specifico. Il valore predefinito è 0, che determina una dimensione del pool illimitata.
1. Nella casella Numero massimo di istanze del servizio asincrone immetti il numero massimo di istanze del pool che è possibile utilizzare per soddisfare le richieste del servizio asincrone in un determinato momento. Questa impostazione consente al servizio di limitare il numero di richieste che può gestire in parallelo.
1. Nella casella Timeout di attesa della chiamata immetti il numero di millisecondi di attesa per la disponibilità di un servizio per una richiesta di chiamata. Se non specifichi un valore per questa impostazione, il valore predefinito è 0 e non viene impostato nessun tempo di attesa.
1. Fai clic su Salva.

### Rimuovere il pooling {#remove-pooling}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizio fai clic sul servizio da configurare.
1. Fai clic sulla scheda Pooling.
1. Nell’elenco Strategia di elaborazione delle richieste, seleziona Nuova istanza per ogni richiesta o Istanza singola per tutte le richieste.

   **Istanza singola per tutte le richieste:** quando la prima richiesta arriva nel contenitore, un’istanza del servizio viene creata e memorizzata nella cache. Ogni richiesta successiva a tale richiesta utilizza la stessa istanza del servizio per gestire la richiesta.

   **Nuova istanza per ogni richiesta:** viene creata una nuova istanza del servizio per ogni chiamata ricevuta.

1. Fai clic su Salva.
