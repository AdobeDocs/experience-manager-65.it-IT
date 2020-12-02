---
title: Configurare le impostazioni del servizio
seo-title: Configurare le impostazioni del servizio
description: Scoprite come configurare le impostazioni del servizio.
seo-description: Scoprite come configurare le impostazioni del servizio.
uuid: e95425a4-62f6-473e-b21b-d081c432e02d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 2fab4b0c-e5db-47cd-b85a-4ff5ad6eb178
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '10710'
ht-degree: 0%

---


# Configurare le impostazioni del servizio {#configure-service-settings}

È possibile utilizzare la pagina Gestione servizi per configurare le impostazioni per ciascuno dei servizi che fanno parte di AEM moduli. Le impostazioni disponibili variano a seconda del servizio configurato.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Arrestate il servizio prima di modificarlo. (Vedere [Avvio e arresto dei servizi](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
1. Fate clic sul nome del servizio che desiderate configurare.
1. Se il servizio dispone di una scheda Configurazione, utilizzatela per modificare le impostazioni del servizio. Per ulteriori informazioni, consulta l’elenco dei collegamenti riportato di seguito.

   >[!NOTE]
   >
   >Non tutti i servizi elencati nella pagina Gestione servizi dispongono di una scheda Configurazione. Per i processi creati dall&#39;utente, la scheda Configurazione viene visualizzata solo se è stato aggiunto un parametro di configurazione al processo in Workbench. (Vedere &quot;Parametri di configurazione&quot; nella Guida di [Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) .)


1. Fare clic sulla scheda Protezione e impostare le impostazioni di protezione per il servizio. Vedere [Modifica delle impostazioni di protezione per un servizio](configure-service-settings.md#modifying-security-settings-for-a-service).
1. Se il servizio dispone di una scheda Endpoint, utilizzatela per modificare le impostazioni dell&#39;endpoint. Vedere [Gestione di endpoint](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md).
1. Fate clic sulla scheda Pool e impostate le impostazioni di pooling. Vedere [Configurazione del pool per un servizio](configure-service-settings.md#configuring-pooling-for-a-service).
1. Fate clic su Salva per salvare le modifiche o su Annulla per eliminarle.
1. Selezionate la casella di controllo accanto al nome del servizio e fate clic su Avvia per riavviare il servizio.

## Impostazioni del servizio Flusso di lavoro di controllo {#audit-workflow-service-settings}

Workbench consente di registrare le istanze del processo durante l&#39;esecuzione in fase di esecuzione e quindi di riprodurle per osservare il funzionamento del processo. (Vedere [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).) Per risparmiare spazio sul file system del server dei moduli, è possibile limitare la quantità di dati di registrazione dei processi memorizzati. È possibile configurare le seguenti proprietà del servizio di controllo del flusso di lavoro ( `AuditWorkflowService`):

**maxNumberOfRecordingInstances:** Il numero massimo di registrazioni memorizzate. Quando viene memorizzato il numero massimo, la registrazione più vecchia viene rimossa dal file system quando viene creata una nuova registrazione. Questa proprietà è utile se si tende a creare molte registrazioni e si desidera rimuovere automaticamente le vecchie registrazioni. Il valore predefinito è 50.

**MaxNumberOfRecordingEntries:** Il numero massimo di voci di dati che possono essere memorizzate per ciascuna registrazione. Le voci di dati sono informazioni sulle operazioni in corso di elaborazione. Varie voci sono memorizzate per ogni esecuzione di un&#39;operazione, ad esempio se l&#39;operazione è iniziata, se l&#39;operazione è stata completata e se il percorso che porta all&#39;operazione è completo. Questa proprietà è utile quando i processi possono includere molte esecuzioni di operazioni, ad esempio, quando viene rilevato un ciclo infinito. Il valore predefinito è 50.

## impostazioni del servizio moduli codici a barre {#barcoded-forms-service-settings}

Il servizio di moduli con codice a barre `(BarcodedFormsService)` estrae i dati del codice a barre dalle immagini scansionate. Il servizio accetta un modulo con codice a barre (TIFF o PDF) come input ed estrae la rappresentazione macchina dei dati codificati dai codici a barre.

Per il servizio moduli con codice a barre sono disponibili le seguenti impostazioni.

**Lettura a sinistra:** se questa opzione è selezionata, le immagini del codice a barre vengono acquisite in orizzontale da destra a sinistra.

**Lettura a destra:** se è selezionata questa opzione, le immagini del codice a barre vengono digitalizzate in orizzontale da sinistra a destra.

**Lettura in alto:** se è selezionata questa opzione, le immagini del codice a barre vengono digitalizzate verticalmente dal basso verso l&#39;alto.

**Lettura in basso:** se è selezionata questa opzione, le immagini del codice a barre vengono digitalizzate verticalmente dall&#39;alto verso il basso.

>[!NOTE]
>
>Per impostazione predefinita, tutte le opzioni sono selezionate. Deselezionare un&#39;opzione solo se si è certi che sui moduli non verrà visualizzato alcun codice a barre.

**Percorso file di base:** percorso del file relativo ai parametri di input e di output del batch per le operazioni Esegui processo file XML ed Esegui processo file semplice. Nelle configurazioni cluster, il percorso del file di base deve essere un percorso del file system condiviso a cui tutti i nodi del cluster hanno accesso in lettura/scrittura.

**Nome origine dati:** nome dell&#39;origine dati utilizzata per mantenere le informazioni sullo stato e sulla cronologia dei processi di elaborazione batch. L&#39;origine dati specificata deve supportare transazioni globali (XA).

## Impostazioni del servizio Central Migration Bridge (obsoleto) {#central-migration-bridge-service-settings}

Il servizio Central Migration Bridge ( `CentralMigrationBridge`) richiama un sottoinsieme di funzionalità Adobe Central Pro Output Server (Central) , che include i comandi JFMERGE, JFTRANS e XMLIMPORT. Le operazioni del servizio Ponte di migrazione centrale consentono di riutilizzare le risorse Central seguenti nei moduli AEM:

* progettazione di modelli (&amp;ast;.ifd)
* modelli di output (&amp;ast;.mdf)
* file di dati (&amp;ast;.dat, file)
* file preambolo (&amp;ast;.pre)
* file di definizione dei dati (&amp;ast;.tdf)

Per il servizio Central Migration Bridge è disponibile la seguente impostazione.

**Directory di installazione centrale:** La directory in cui è installato  Adobe Central 5.7.

## Connettore dell&#39;archivio dei contenuti per le impostazioni del servizio EMC Documentum {#content-repository-connector-for-emc-documentum-service-settings}

Content Repository Connector per il servizio EMC Documentum ( `EMCDocumentumContentRepositoryConnector`) consente di creare processi che interagiscono con il contenuto memorizzato in un repository Documentum.

La seguente impostazione è disponibile per il connettore Content Repository per il servizio EMC Documentum.

**Percorso predefinito oggetto collegamento risorsa:** La parte predefinita del percorso nell&#39;archivio Documentum per la memorizzazione dell&#39;oggetto Collegamento risorsa. Il percorso effettivo è costituito dal percorso predefinito e dalla posizione del modello di modulo nell&#39;archivio moduli AEM.

Ad esempio, se il percorso predefinito è impostato su `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects` e il modello di modulo è memorizzato in una cartella `/Docbase/forms/`, l’oggetto Collegamento risorsa viene memorizzato nel percorso seguente:

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

Il valore predefinito di questa impostazione è `/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`.

## Content Repository Connector for IBM FileNet service settings {#content-repository-connector-for-ibm-filenet-service-settings}

Content Repository Connector for IBM FileNet consente di creare processi che interagiscono con il contenuto memorizzato in un archivio IBM FileNet.

La seguente impostazione è disponibile per Content Repository Connector per il servizio FileNet IBM.

**Percorso predefinito oggetto collegamento risorsa:** la parte predefinita del percorso nell&#39;archivio FileNet di IBM per la memorizzazione dell&#39;oggetto Collegamento risorsa. Il percorso effettivo è costituito dal percorso predefinito e dalla posizione del modello di modulo nell&#39;archivio moduli AEM.

Ad esempio, se il percorso predefinito è impostato su `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects` e il modello di modulo è memorizzato in una cartella `/Docbase/forms/`, l’oggetto Collegamento risorsa viene memorizzato nel percorso seguente:

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

Il valore predefinito di questa impostazione è `/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`.

## Converti impostazioni servizio PDF {#convert-pdf-service-settings}

Il servizio Converti PDF ( `ConvertPdfService`) converte i documenti PDF in PostScript e in diversi formati di immagine (JPEG, JPEG 2000, PNG e TIFF). La conversione di un documento PDF in PostScript è utile per la stampa automatica basata su server su qualsiasi stampante PostScript. La conversione di un documento PDF in un file TIFF multipagina è pratica quando si archiviano documenti in sistemi di gestione dei contenuti che non supportano documenti PDF.

Per il servizio Converti PDF sono disponibili le seguenti impostazioni.

**Tipo di transazione:** specifica in che modo il contesto di una transazione deve essere propagato a un&#39;operazione.

**Obbligatorio:** supporta un contesto di transazione, se esistente; in caso contrario, viene creato un nuovo contesto di transazione. Questo è il valore predefinito.

**Richiede Nuovo: crea** sempre un nuovo contesto di transazione. Se esiste un contesto di transazione attivo, viene sospeso.

**Timeout transazione (in secondi):** il numero di secondi di attesa del provider di transazioni sottostante prima del rollback di una transazione con wrapping dell&#39;operazione. Questo valore verrà ignorato se viene propagato un contesto di transazione esistente. Il valore predefinito è 180.

**Risoluzione soglia per l&#39;arrotondamento (in dpi):** la risoluzione dell&#39;immagine al di sotto della quale l&#39;uniformità (o l&#39;anti-alias) viene applicata al testo, alla grafica e alle immagini, se avete selezionato le opzioni &quot;Applica arrotondamento a&quot; per tali elementi.

**Applicazione dell’arrotondamento al testo:** Controlla l’anti-alias del testo. Per disattivare l’arrotondamento del testo e rendere il testo più nitido e leggibile con una lente di ingrandimento dello schermo, deselezionare questa casella di controllo.

**Applicazione dell&#39;uniformità a LineArt:** applica l&#39;uniformità per rimuovere angoli bruschi nelle linee.

**Applicazione dell’uniformità alle immagini:** Applica l’arrotondamento per ridurre al minimo le modifiche brusche apportate alle immagini.

## Impostazioni del servizio Distiller {#distiller-service-settings}

Il servizio Distiller ( `DistillerService`) converte i file PostScript, Encapsulated PostScript (EPS) e PRN in file PDF in rete.

Le seguenti impostazioni sono disponibili per il servizio Distiller.

**impostazioni Adobe PDF:** al PDF generato vengono applicate le seguenti impostazioni preconfigurate:

* Stampa di alta qualità
* Pagine oversize
* PDFA1b 2005 CMYK
* PDFA1b 2005 RGB
* PDFX1a 2001
* PDFX3 2002
* Qualità della stampa
* Dimensione file minima
* Standard

È possibile creare nuove impostazioni tramite l&#39;interfaccia utente di PDF Generator.

**Impostazioni di protezione:impostazioni di protezione** preconfigurate applicate ai documenti PDF generati. Il valore predefinito è Nessuna protezione. È necessario creare le impostazioni di protezione utilizzando PDF Generator, quindi immettere l&#39;impostazione qui.

**Dimensione pool:** la dimensione iniziale del pool. Quando il servizio Distiller viene distribuito, questo numero viene utilizzato per determinare il numero di istanze di implementazione del servizio che vengono create e allocate al pool gratuito in attesa delle richieste di chiamata. Il contenitore del servizio può quindi rispondere immediatamente alle richieste di chiamata senza dover prima inizializzare un&#39;istanza del servizio.

## Impostazioni del servizio Gestione documenti {#document-management-service-settings}

>[!NOTE]
>
> Adobe® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle LiveCycle®. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulle persone. Il supporto di Content Services (obsoleto) termina il 31/12/2014. Vedere [ documento sul ciclo di vita del prodotto del Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Per informazioni sulla configurazione di Content Services (obsoleto), vedere [Amministrazione di Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

Il servizio Document Management ( `DocumentManagementService`) consente ai processi di utilizzare la funzionalità di gestione dei contenuti fornita da Content Services (obsoleto). Le operazioni di gestione dei documenti forniscono le attività di base necessarie per mantenere spazi e contenuti nel sistema di gestione dei contenuti. Esempi di tali attività sono copiare, eliminare, spostare, recuperare e archiviare contenuti, creare spazi e associazioni e ottenere e impostare gli attributi di contenuto.

Per il servizio Gestione documenti sono disponibili le seguenti impostazioni.

**Schema store:** lo schema dello store in cui si trova il contenuto. Il valore predefinito è workspace.

**Porta HTTP:** la porta utilizzata per accedere a Content Services (obsoleto). Il valore predefinito è 8080.

## Impostazioni del servizio e-mail {#email-service-settings}

Le e-mail vengono comunemente utilizzate per distribuire contenuti o fornire informazioni sullo stato come parte di un processo automatizzato. Il servizio e-mail ( `EmailService`) consente ai processi di ricevere messaggi e-mail da un server POP3 o IMAP e di inviare messaggi e-mail a un server SMTP.

Ad esempio, un processo utilizza il servizio E-mail per inviare un messaggio e-mail contenente un allegato del modulo PDF. Il servizio e-mail si connette a un server SMTP per inviare il messaggio e-mail con l&#39;allegato. Il modulo PDF è progettato per consentire al destinatario di fare clic su Invia dopo aver completato il modulo. Questa azione causa la restituzione del modulo come allegato al server di posta elettronica designato. Il servizio e-mail recupera il messaggio e-mail restituito e memorizza il modulo compilato in una variabile del modulo di dati del processo.

Per il servizio e-mail sono disponibili le seguenti impostazioni.

**Host SMTP:** L&#39;indirizzo IP o l&#39;URL del server SMTP da utilizzare per l&#39;invio dell&#39;e-mail.

**Numero di porta SMTP:** La porta utilizzata per connettersi al server SMTP.

**Autenticazione SMTP:** selezionare se per connettersi al server SMTP è necessaria l&#39;autenticazione utente.

**Utente SMTP:** Il nome utente dell&#39;account utente da utilizzare per accedere al server SMTP.

**Password SMTP:** La password associata all&#39;account utente SMTP.

**Protezione trasporto SMTP:** Il protocollo di sicurezza da utilizzare per la connessione al server SMTP:

* Seleziona Nessuno se non viene utilizzato alcun protocollo (i dati vengono inviati in testo non crittografato)
* Selezionate SSL se viene utilizzato il protocollo Secure Sockets Layer.
* Selezionate TLS se viene utilizzata la sicurezza del livello di trasporto.

**Host POP3/IMAP:** L&#39;indirizzo IP o l&#39;URL del server POP3 o IMAP da utilizzare per l&#39;invio di e-mail.

**Nome utente POP3/IMAP:** il nome utente dell&#39;account utente da utilizzare per accedere al server POP3 o IMAP.

**Password POP3/IMAP:** la password associata all&#39;account utente POP3 o IMAP.

**Numero porta POP3/IMAP:** la porta utilizzata per connettersi al server POP3 o IMAP.

**POP3/IMAP:** Protocollo da utilizzare per inviare e ricevere e-mail.

**Ricevi sicurezza trasporto:** il protocollo di sicurezza da utilizzare per la connessione al server SMTP:

* Selezionare Nessuno se non viene utilizzato alcun protocollo (i dati vengono inviati in testo non crittografato).
* Selezionate SSL se viene utilizzato il protocollo Secure Sockets Layer.
* Selezionate TLS se viene utilizzata la sicurezza del livello di trasporto.

## Impostazioni del servizio di cifratura {#encryption-service-settings}

Il servizio di cifratura ( `EncryptionService`) consente di cifrare e decrittografare i documenti. Quando un documento viene crittografato, il relativo contenuto diventa illeggibile. Un utente autorizzato può decifrare il documento per ottenere l&#39;accesso ai contenuti. Se un documento PDF è crittografato con una password, l&#39;utente deve specificare la password aperta per poter visualizzare il documento in  Adobe Reader o  Adobe Acrobat. Analogamente, se un documento PDF è crittografato con un certificato, l&#39;utente deve decrittografare il documento PDF con la chiave pubblica che corrisponde al certificato (chiave privata) utilizzato per cifrare il documento PDF.

Per il servizio di cifratura sono disponibili le seguenti impostazioni.

**Server LDAP predefinito a cui connettersi:nome** host del server LDAP utilizzato per recuperare i certificati per la cifratura del documento.

**Porta LDAP predefinita a cui connettersi:numero di** porta del server LDAP.

**Nome utente LDAP predefinito:** se il server LDAP richiede l’autenticazione, specificate il nome utente da usare per la connessione al server LDAP.

**Password LDAP predefinita:** se il server LDAP richiede l’autenticazione, specificate la password che corrisponde al nome utente da utilizzare per connettersi al server LDAP.

>[!NOTE]
>
>Utilizzate l&#39;autenticazione semplice (nome utente e password) solo quando la connessione è protetta tramite SSL (tramite LDAPS).

**Modalità compatibilità:**

## Impostazioni del servizio FTP {#ftp-service-settings}

Il servizio FTP ( `FTP`) consente ai processi di interagire con un server FTP. Le operazioni del servizio FTP possono recuperare i file dal server FTP, caricare i file sul server FTP ed eliminare i file dal server FTP. Ad esempio, documenti come i report generati da un processo possono essere memorizzati in un server FTP per la distribuzione. Oppure, un sistema esterno potrebbe generare alcuni file basati sui passaggi precedenti di un processo. In una fase successiva del processo, i file possono essere trasferiti in una posizione remota.

Le seguenti impostazioni sono disponibili per il servizio FTP.

**Host predefinito:** l&#39;indirizzo IP o l&#39;URL del server FTP.

**Porta predefinita:** la porta utilizzata per connettersi al server FTP. Il valore predefinito è 21.

**Nome utente predefinito:** il nome dell&#39;account utente che potete utilizzare per accedere al server FTP. L&#39;account utente deve disporre di privilegi sufficienti per eseguire le operazioni FTP richieste dal servizio.

**Password predefinita:** la password da utilizzare con il nome utente specificato per l&#39;autenticazione con il server FTP.

## Genera impostazioni servizio PDF {#generate-pdf-service-settings}

Il servizio Genera PDF ( `GeneratePDFService`) converte i file in vari formati nativi in documenti PDF e converte i documenti PDF in diversi formati di file.

Per il servizio Genera PDF sono disponibili le seguenti impostazioni.

**impostazioni Adobe PDF:** il nome delle impostazioni Adobe PDF  preconfigurate da applicare a un processo di conversione, se queste impostazioni non vengono specificate come parte dei parametri di chiamata API. Le  impostazioni Adobe PDF sono configurate nella console di amministrazione, facendo clic su Servizi > PDF Generator >  Impostazioni Adobe PDF. Queste impostazioni sono applicabili solo alle conversioni basate su PDFMaker.

**Impostazioni di protezione:** il nome delle impostazioni di protezione preconfigurate da applicare a un processo di conversione, se queste impostazioni non vengono specificate come parte dei parametri di chiamata API. Le impostazioni di protezione sono configurate nella console di amministrazione, facendo clic su Servizi > PDF Generator > Impostazioni di protezione.

**Tipo di file Impostazioni:** il nome dell&#39;impostazione del tipo di file preconfigurata da applicare a un processo di conversione, se queste impostazioni non vengono specificate come parte dei parametri di chiamata API. Le impostazioni relative ai tipi di file sono configurate nella console di amministrazione facendo clic su Servizi > Generatore PDF > Impostazioni tipo di file.

**Usa  Acrobat WebCapture (solo Windows):** quando questa impostazione è true, il servizio Genera PDF utilizza  Acrobat X Pro per tutte le conversioni da HTML a PDF. Ciò può migliorare la qualità dei file PDF prodotti da HTML, anche se le prestazioni potrebbero essere leggermente inferiori. Il valore predefinito è false.

**Usa  conversione immagine Acrobat (solo Windows):** quando questa impostazione è true, il servizio Genera PDF utilizza  Acrobat X Pro per tutte le conversioni da immagine a PDF. Questa impostazione è utile solo se il meccanismo predefinito di conversione Java pura non è in grado di convertire correttamente una parte significativa delle immagini di input. Il valore predefinito è false.

**Abilita  conversioni AutoCAD basate su Acrobat (solo Windows):** quando questa impostazione è true, il servizio Genera PDF utilizza  Acrobat X Pro per tutte le conversioni da DWG a PDF. Questa impostazione è utile solo se AutoCAD non è installato sul server o se il meccanismo di conversione AutoCAD non è in grado di convertire i file.

**Espressioni regolari per la ricerca di caratteri speciali vietati nel nome utente (solo Windows):** specifica i caratteri che interferiscono con le operazioni di Optimize PDF  e  quando i caratteri compaiono nel nome di un utente.

**Dimensione pool ImageToPDF:** Dimensione pool del convertitore predefinito da immagine a PDF (Java puro) nel servizio Genera PDF. Questa impostazione controlla il numero massimo simultaneo di conversioni da immagine a PDF eseguibili dal servizio Genera PDF. Il valore predefinito di questa impostazione (consigliato per i sistemi a processore singolo) è 3, che può aumentare sui sistemi multiprocessore.

**Dimensione pool da HTML a PDF:** dimensione pool del convertitore da HTML a PDF nel servizio Genera PDF. Questa impostazione controlla il numero massimo simultaneo di conversioni da HTML a PDF eseguibili dal servizio Genera PDF. Il valore predefinito di questa impostazione (consigliato per i sistemi a processore singolo) è 3, che può aumentare sui sistemi multiprocessore.

**Dimensione pool OCR:** dimensione pool del PaperCaptureService utilizzato da PDF Generator per OCR. Il valore predefinito di questa impostazione (consigliato per i sistemi a processore singolo) è 3, che può aumentare sui sistemi multiprocessore. Questa impostazione è valida solo sui sistemi Windows.

**Famiglia di font di fallback per le conversioni da HTML a PDF:** il nome della famiglia di font da utilizzare nei documenti PDF quando il font utilizzato nell&#39;HTML originale non è disponibile per il server moduli AEM. Specificate una famiglia di font se intendete convertire le pagine HTML che utilizzano font non disponibili. Ad esempio, le pagine create in lingue regionali potrebbero utilizzare font non disponibili.

**Logica di ripetizione per** le conversioni nativeGoverna i tentativi di generazione PDF se il primo tentativo di conversione non è riuscito:

**Nessun tentativo**

Non riprovare la conversione PDF se il primo tentativo di conversione non è riuscito

**Riprova**

Riprovare la conversione PDF indipendentemente dal raggiungimento della soglia di timeout. La durata di timeout predefinita per il primo tentativo è 270 s.

**Riprova se il tempo a disposizione lo consente**

Riprovare la conversione PDF se il tempo utilizzato per il primo tentativo di conversione è inferiore alla durata di timeout specificata. Ad esempio, se la durata di timeout è 270 e il primo tentativo è stato consumato 200 secondi, PDF Generator tenterà nuovamente di convertire. Se il primo tentativo è stato utilizzato per 270 secondi, la conversione non verrà tentata nuovamente.

## Impostazioni del servizio Guide ES4 Utilities {#guides-es4-utilities-service-settings}

Quando si crea una Guida, alcune risorse, come la definizione della Guida, vengono incorporate nella Guida. Le risorse possono essere anche utilizzate come riferimenti alle risorse dell&#39;applicazione memorizzate localmente o sul server AEM moduli. La Guida non contiene dati e i valori per la posizione di invio e gli input non sono adatti a tutti gli ambienti esterni.

Nella maggior parte dei casi, i servizi di rendering Guide predefiniti sono sufficienti per preparare una Guida da utilizzare in Workspace o in altri ambienti esterni. (Nella visualizzazione Servizi, in Workbench, il servizio predefinito è Guide (sistema)/Processi/Guida di rendering - 1.0.) Il servizio Guide Utilities ( `GuidesUtility`) consente di creare un processo personalizzato per il rendering di una Guida TV, se necessario.

Le operazioni Guide Utilities (Utilità guida) consentono di aggiungere le seguenti attività di rendering Guide a un processo:

* Determinare se i dati sono disponibili per compilare la Guida con
* Incorporare i dati della Guida o convertirli in un collegamento
* Conversione del contenuto di riferimento in URL con accesso esterno
* Sostituire i valori in un documento HTML o in un altro wrapper, o convertirli in URL con accesso esterno
* Impostare il percorso di invio
* Specificare i valori di input
* Creare un parametro per rappresentare il contenuto a cui si fa riferimento
* Se sono disponibili delle variazioni, imposta una variazione

I valori predefiniti per il servizio Guide Utilities supportano la maggior parte dei casi di utilizzo. Tuttavia, se necessario, potete modificare i seguenti valori.

**publicPaths:** Questa opzione è stata rimossa. Non utilizzare questa opzione con AEM moduli.

**pathInfoExpiryInSeconds:** L’intervallo dopo il quale scade una richiesta di informazioni sul percorso da parte di un client. Il valore predefinito è 1.

**collateraleExpiryInSeconds:** l&#39;intervallo dopo il quale scade una richiesta di garanzia da parte di un cliente. Il valore predefinito è 315576000.

**mismatchExpiryInSeconds:** L’intervallo dopo il quale scade una richiesta di garanzia da un client, quando l’eTag (tag entità) non corrisponde. Un eTag è un’intestazione di risposta HTTP. Il valore predefinito è 1.

**guideContext:** radice contestuale dell’applicazione Web Guide. Corrisponde al valore impostato utilizzando l&#39;applicazione Web Guide. Il valore predefinito è /Guides/.

**secureRandomAlgorithm:** l&#39;algoritmo da utilizzare per la generazione di chiavi e identificatori. Questo valore viene passato al metodo getInstance della classe Java SecureRandom. Il valore predefinito è SHA1PRNG.

**idBytes:** il numero di byte casuali da utilizzare per un identificatore chiave. Il valore predefinito è 6.

**macAlgorithm:** l&#39;algoritmo MAC (codice di autenticazione dei messaggi) da utilizzare per la verifica degli URL collaterali. Questo metodo viene passato al metodo getInstance della classe Mac. Il valore predefinito è HmacSHA1.

**macRefreshIntervalInMinutes:** la quantità di tempo in cui una chiave è attiva. Quando una chiave è stata attiva per questo intervallo, viene generata una nuova chiave. La nuova chiave diventa la chiave attiva. La chiave precedentemente attiva viene mantenuta per il 10% dell&#39;intervallo di aggiornamento. Questo comportamento consente agli URL generati utilizzando la chiave precedente di continuare a funzionare nello switch chiave. Il valore predefinito è 144000.

**macOverlapIntervalInMinutes:** tempo entro il quale la chiave precedente rimarrà valida dopo la generazione di una nuova chiave. Il valore predefinito è 1440 minuti (1 giorno).

**macKeySeed:** un valore seed per la generazione dell&#39;URL protetto. Quando questa opzione è selezionata, la chiave non viene mai aggiornata. Se si imposta lo stesso valore sui diversi server, i server genereranno URL sicuri compatibili. Ciò può essere utile se dietro un sistema di bilanciamento del carico sono in uso più server di moduli. Immettete una sequenza casuale di caratteri e numeri come valori iniziali.

### Utilizzo delle guide in un cluster di server {#using-guides-in-a-server-cluster}

Il rendering di una Guida in un cluster di server che non utilizza sessioni fisse non riesce con NullPointerException. Una richiesta Guide utilizza gli URL protetti che, per impostazione predefinita, sono univoci per il server in cui sono generati. In un cluster che utilizza le sessioni fisse, dopo che una richiesta ha toccato un nodo del cluster, tutte le richieste successive per tale sessione o utente vengono instradate esclusivamente a tale server, e tutto va bene. In un cluster che non utilizza sessioni fisse, le richieste successive possono colpire qualsiasi server del cluster. Se il server a cui hanno risposto le richieste non è il server originale, l&#39;URL protetto non verrà risolto.

Se si utilizzano le Guide in un cluster di server che non utilizza le sessioni di sticky, impostare il valore macKeySeed per il servizio GuidesUtility, quindi arrestare e avviare il cluster.

Il valore macKeySeed è l’elemento di base per il generatore di numeri casuali utilizzato per generare gli URL protetti. Impostando questo valore, ogni nodo del cluster inizializza il generatore di numeri casuali allo stesso modo e ha accesso agli stessi URL protetti. È possibile utilizzare qualsiasi stringa casuale per questo valore di inizializzazione.

Modificate il valore macKeySeed quando è necessario aggiornare gli URL protetti. L&#39;aggiornamento degli URL protetti dipende dal criterio di protezione in uso ed è simile al criterio di aggiornamento per la modifica della password principale del server. macSeedValue è simile alla password master per gli URL protetti, in quanto viene utilizzata per generare un nuovo numero casuale univoco da utilizzare per la generazione e il recupero sicuri degli URL.

È necessario riavviare il cluster perché macSeedValue è di sola lettura all&#39;avvio del sistema. Per leggere il valore è necessario riavviare tutti i nodi, in quanto essi lo utilizzano in modo indipendente per inizializzare i numeri casuali interni con il valore seed.

## Impostazioni del servizio JDBC {#jdbc-service-settings}

Il servizio JDBC ( `JdbcService`) consente ai processi di interagire con i database.

Per il servizio JDBC è disponibile la seguente impostazione.

**datasourceName:** Valore di stringa che rappresenta il nome JNDI dell&#39;origine dati da utilizzare per connettersi al server del database. L&#39;origine dati deve essere definita nel server dell&#39;applicazione che ospita il server dei moduli. Il valore predefinito è il nome JNDI dell&#39;origine dati per il database dei moduli AEM.

## Impostazioni del servizio JMS {#jms-service-settings}

Il servizio JMS ( `JMS`) consente l&#39;interazione con i provider JMS (Java Messaging System) che implementano sia messaggi point-to-point che messaggi di pubblicazione/sottoscrizione.

Configurate il servizio JMS con le proprietà predefinite in modo che le operazioni del servizio possano connettersi e interagire con un provider JMS e un servizio JNDI associato. I valori delle proprietà del servizio sono impostati su valori predefiniti basati sul server applicazioni JBoss. Modificare questi valori se si utilizza un server applicazione diverso per ospitare AEM moduli.

Le seguenti impostazioni sono disponibili per il servizio JMS.

**URL provider:** l&#39;URL del provider di servizi JNDI. Il valore predefinito si basa sul server applicazioni JBoss. L&#39;URL seguente è un valore predefinito per i server applicazione supportati AEM moduli:

**JBoss:** `<server name>:1099`

**WebLogic:** `<server name>:7001`

**WebSphere:** `<server name>:2809`

**Nome utente JNDI:** il nome utente dell&#39;account da utilizzare per l&#39;autenticazione con il provider di servizi JNDI che viene utilizzato per cercare i nomi degli argomenti e delle code. Il valore predefinito è guest.

**Password JNDI:** la password associata al nome utente specificato per il nome utente JNDI. Il valore predefinito è guest.

**Context Factory iniziale:** la classe Java da utilizzare come context factory iniziale. Il servizio JMS utilizza questa classe per creare un contesto iniziale, che rappresenta il punto di partenza per la risoluzione dei nomi di argomenti e code. Il valore predefinito è il context factory iniziale per il servizio JMS su JBoss. Le classi seguenti sono i context factory iniziali per i server applicazioni che AEM i moduli supportano:

**JBoss:** org.jnp.interface.NamingContextFactory

**WebLogic:** weblogic.jndi.WLInInitialContextFactory

**WebSphere:** com.ibm.webfers.name.WsnInitialContextFactory

**Nome utente connessione:** la password associata al nome utente specificato per Nome utente connessione. Il valore predefinito è guest.

**Password connessione:** la password associata al nome utente specificato per Nome utente connessione. Il valore predefinito è guest.

**Altre proprietà:coppie nome e valore** proprietà che è possibile trasmettere al provider di servizi JNDI. Tali proprietà dipendono dall’implementazione e dalla configurazione del provider in uso.

Le coppie nome/valore delle proprietà sono separate da due punti e virgola **;**. Ad esempio, il testo seguente mostra il valore che verrebbe specificato per due proprietà denominate name1 e name2, rispettivamente con i valori value1 e value2:

`name1=value1;name2=value2`

## Impostazioni del servizio LDAP {#ldap-service-settings}

Il servizio LDAP ( `LDAPService`) fornisce le operazioni necessarie per eseguire query sulle directory LDAP. Le directory LDAP vengono in genere utilizzate per memorizzare informazioni sulle persone, i gruppi e i servizi di un’organizzazione.

Per il servizio LDAP sono disponibili le seguenti impostazioni.

**Context Factory iniziale:** classe Java da utilizzare come context factory. Questa classe viene utilizzata per creare una connessione al server LDAP. Il valore predefinito è com.sun.jndi.ldap.LdapCtxFactory, appropriato per la maggior parte dei server LDAP.

**URL fornitore:** l’URL da usare per la connessione al servizio LDAP. Il formato del valore è `ldap://server name:port`

*nome server* è il nome del computer che ospita il server LDAP

*Porte* è la porta di comunicazione utilizzata dal servizio LDAP. Il valore predefinito è 389, ovvero la porta standard utilizzata per le connessioni LDAP.

**Nome utente:** il nome utente dell’account utente da utilizzare per accedere al server LDAP. L’account utente deve disporre dell’autorizzazione per connettersi al server e leggere le informazioni presenti nella directory LDAP.

A seconda del server LDAP, il nome utente può essere un semplice nome utente, ad esempio `myname` o un DN, ad esempio `cn=myname,cn=users,dc=myorg`.

**Password:** la password che corrisponde al nome utente fornito per l’impostazione Nome utente.

**Altre proprietà:** valore di stringa che rappresenta altre proprietà e i relativi valori che potete fornire al server LDAP. Il valore è nel seguente formato:

`property=value;property=value;...`

## Impostazioni del servizio di configurazione di Microsoft SharePoint {#microsoft-sharepoint-configuration-service-settings}

Il servizio di configurazione di Microsoft SharePoint `(MSSharePointConfigService)`consente di specificare le credenziali per l&#39;utente dei moduli AEM che dispone delle autorizzazioni di rappresentazione. Per informazioni sulle autorizzazioni di rappresentazione, vedere [Configurazione del connettore per Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html).

Sono disponibili le seguenti impostazioni per il servizio di configurazione di Microsoft SharePoint:

* Nome utente per un utente con autorizzazioni di rappresentazione
* Password per l’utente sopra indicato

**Abilita SSL (HTTPS):**

**Tempo di esecuzione:** durata, in secondi, del tempo in cui il profilo di provisioning è valido e memorizzato nella cache del client. Il valore predefinito è 86400 (24 ore). Quando un&#39;applicazione client si sincronizza con il server e il tempo specificato è trascorso, l&#39;applicazione client richiede un nuovo profilo di provisioning dal server.

**Cifratura:** specifica se cifrare i dati memorizzati sul dispositivo mobile.

**Applicazione Forms:** abilita la funzione Forms nelle applicazioni client per dispositivi mobili. Quando questa opzione è selezionata, gli utenti possono aprire i moduli e avviare processi dai propri dispositivi mobili.

**Applicazione attività:** abilita la funzione Attività nelle applicazioni client per dispositivi mobili. Quando questa opzione è selezionata, gli utenti possono accedere agli elenchi delle attività e completare le attività dai propri dispositivi mobili.

**Applicazione Content Services:** abilita la funzione Content Services nell&#39;applicazione client per dispositivi mobili. Questa funzione è disponibile solo per iOS. Quando questa opzione è selezionata, gli utenti iPhone e iPad possono accedere ai file memorizzati nel server WebDAV aziendale.

**Supporto offline:** consente agli utenti di continuare a utilizzare le applicazioni client mobili anche quando non dispongono di una connessione al server (ad esempio, quando non rientrano nell&#39;intervallo di celle o in modalità aereo). Gli utenti devono inoltre abilitare l&#39;impostazione Supporto offline sui loro dispositivi mobili. Questa funzione è disponibile per i dispositivi Android e iOS. Per impostazione predefinita, questa funzione è disattivata.

>[!NOTE]
>
>Se il supporto offline è stato abilitato e successivamente lo si disabilita, i profili di provisioning degli utenti vengono aggiornati immediatamente o non appena sono online. Se un utente ha lavorato offline, tutte le attività in sospeso vengono riportate nell&#39;elenco Attività e tutti gli elementi nella coda, inclusi moduli in sospeso, attività e moduli contenenti errori di convalida, vengono eliminati dalla coda.

**Android:** consente ai dispositivi Android di connettersi al server.

**Apple iOS:** consente agli iPhone e agli iPad di connettersi al server.

**AIR:** consente ai dispositivi che eseguono app basate su  Adobe AIR® di connettersi al server.

**BlackBerry:** Consente ai dispositivi BlackBerry di connettersi al server.

**Android Microsoft Exchange ActiveSync Obbligatorio:** specifica se Microsoft Exchange ActiveSync Policy Manager (EA) deve essere installato e attivo sui dispositivi Android. Quando questa opzione è selezionata, EA deve essere applicata al dispositivo Android. Se questa opzione non è selezionata, non viene eseguito alcun controllo, anche se altri requisiti sono ancora applicati.

**Lunghezza minima PIN per Android: i dispositivi** Android devono avere un&#39;impostazione globale che applica che il PIN o la password sia almeno di questa lunghezza. Non è sufficiente avere un PIN della lunghezza specificata. La lunghezza del PIN deve essere applicata dal sistema in modo che gli utenti non possano rimuoverlo o accorciarlo in un secondo momento. Il valore predefinito è 4.

**Numero massimo di tentativi di password Android prima di comparsa:i dispositivi** Android hanno un&#39;impostazione globale che cancella il sistema dopo un numero specificato di tentativi di password non validi. Questa impostazione globale è abilitata e uguale o inferiore al valore specificato qui. Il valore predefinito è 5.

**Android Wipe On Removal:** specifica cosa accade quando si verifica una violazione di criteri su un dispositivo Android. Quando questa opzione è selezionata, l&#39;account viene eliminato. Se questa opzione non è selezionata, la password dell&#39;account memorizzato e i dati memorizzati nella cache vengono eliminati. Non vengono più eseguiti tentativi di sincronizzazione finché l&#39;utente non risolve la violazione del criterio.

## Impostazioni del servizio di output {#output-service-settings}

Il servizio Output `(OutputService)`consente di unire i dati del modulo XML a una struttura del modulo creata AEM Designer per creare un flusso di output del documento in uno dei seguenti formati:

* Flusso di output di un documento PDF o PDF/A.
* Un flusso di output Adobe PostScript .
* Flusso di output PCL (Printer Control Language).
* Flusso di output ZPL (Zebra Programming Language).

Il flusso di output può essere inviato a una stampante di rete, a una stampante locale o a un file su disco. Quando si utilizza il servizio Output come parte di un processo, è anche possibile inviare il flusso di output a un destinatario e-mail come file allegato.

Per il servizio Output sono disponibili le seguenti impostazioni.

**Tipo di transazione:** specifica in che modo il contesto di una transazione deve essere propagato a un&#39;operazione:

**Obbligatorio:** supporta un contesto di transazione, se esiste già; in caso contrario, viene creato un nuovo contesto di transazione. Questo è il valore predefinito.

**Richiede Nuovo: crea** sempre un nuovo contesto di transazione. Se esiste un contesto di transazione attivo, viene sospeso.

**Timeout transazione (in secondi):** il numero di secondi di attesa del provider di transazioni sottostante prima del rollback di una transazione che sta eseguendo il wrapping dell&#39;operazione. Questo valore viene ignorato se viene propagato un contesto di transazione esistente.

Quando si elaborano file di dati di grandi dimensioni o si lavora su un server occupato, potrebbe essere necessario aumentare il timeout del servizio Output. Per modificare il valore di timeout, assicurarsi che i server hardware dispongano di memoria adeguata e che la memoria sia disponibile per l&#39;heap Java Application Server. Il valore predefinito è `180`.

## Impostazioni del servizio di configurazione PDFG {#pdfg-config-service-settings}

Per il servizio di configurazione PDFG sono disponibili le seguenti impostazioni ( `PDFGConfigService`).

**Directory opzioni processo utente:** percorso della cartella del file system in cui il servizio c scrive i file delle opzioni di processo accessibili a  Acrobat Pro Extended. Il valore predefinito è [user.home]/Application Data/ Adobe/ Adobe PDF/Settings.

**Directory di avvio di PS:** percorso della cartella del file system in cui vengono salvati i file di avvio richiesti da  Adobe Acrobat Distiller. Il valore predefinito è [user.home]/Application Data/ Adobe/ Adobe PDF/Distiller/Startup.

**File di avvio PS:** il nome del file di avvio richiesto da  Adobe Acrobat Distiller. Il valore predefinito è example.ps.

**Timeout conversione server:** il timeout massimo di conversione del processo (in secondi) per il servizio Genera PDF e il servizio Distiller. Questa impostazione limita il timeout di conversione massimo che è possibile specificare nel file config.xml e nelle pagine della console di amministrazione per PDF Generator. Il valore predefinito è 270.

**Timeout globale server:** durante l&#39;esecuzione di conversioni PDF, un server moduli tiene conto del limite di timeout. Configurate il valore di timeout per risolvere il problema.

**Prefisso opzioni processo:** Prefisso utilizzato dal servizio Genera PDF per anteporre una stringa breve ai file delle opzioni di processo creati temporaneamente per  Acrobat Distiller. Il valore predefinito è pdfg.

**App non Unicode:** Un elenco separato da virgole di nomi di applicazione noti per non poter utilizzare Unicode. Questo elenco è precompilato con i nomi di diverse applicazioni, il cui supporto è preconfigurato in PDF Generator. Se si sceglie di aggiungere il supporto per le conversioni PDF tramite altre applicazioni di terze parti che non supportano Unicode, è necessario aggiungerlo a questo elenco. Il valore predefinito è Autocad,Excel,PowerPoint,Project,Publisher,Visio,Word,WordPerfect.

**Conteggio pool di thread del server:** controlla la dimensione del pool di thread utilizzato internamente dal servizio Genera PDF per soddisfare le richieste di conversione da HTML a PDF che richiedono l&#39;spider (conversione di pagine collegate accessibili dalla pagina principale). Il valore predefinito è 20.

**PDFG Cleanup Scan Seconds (Secondi di di scansione pulizia PDFG):** per informazioni dettagliate, consultate la sezione Job Expirations Seconds (Scadenza processo).

**Secondi scadenza processo:** il servizio Genera PDF elimina i file di input non appena vengono convertiti. I file di output vengono memorizzati temporaneamente, per un periodo di tempo determinato dalle impostazioni Secondi di pulizia PDFG e Secondi scadenza processo.

L’impostazione Secondi scadenza processo specifica la data di scadenza di un file o di una cartella vuota prima che possa essere eliminato. L’impostazione PDFG Cleanup Scan Seconds specifica la frequenza con cui un thread di pulizia esegue la scansione delle cartelle temporanee per i file che possono essere eliminati.

Ad esempio, se l’opzione Secondi scadenza processo è impostata su 100 e Secondi pulizia PDFG è impostata su 200, il thread di pulizia viene eseguito ogni 200 secondi ed elimina i file che sono almeno 100 secondi.

Il valore predefinito dei secondi di pulizia PDFG è `43200` (12 ore). Il valore predefinito di Secondi scadenza processo è `86400` (24 ore).

**Impostazione internazionale predefinita:** utilizzata per ignorare le impostazioni internazionali predefinite (paese + lingua) del server in cui è distribuito il servizio Genera PDF. Se questo parametro non è specificato, le impostazioni internazionali predefinite sono determinate dal sistema operativo in cui il servizio è distribuito. Questo parametro controlla la lingua in cui i messaggi di errore vengono restituiti alle API.

## impostazioni del servizio Data Services del flusso di lavoro moduli {#forms-workflow-data-services-service-settings}

I seguenti servizi estendono i servizi Data Services ed espongono i assemblatori utilizzati da Workspace per comunicare con il server. Non modificate le opzioni di configurazione per questi servizi, a meno che non vi sia stato richiesto di farlo dal supporto  Adobe. Tali servizi non sono destinati all&#39;accesso diretto:

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## Impostazioni del servizio remoto {#remoting-service-settings}

La maggior parte dei servizi sono configurati in modo da potervi accedere tramite (obsoleto per AEM moduli) AEM moduli Remoting. Per informazioni su (obsoleto per AEM moduli) AEM moduli Remoting, vedere [Programmazione con moduli AEM](https://adobe.com/go/learn_aemforms_programming_63).

Le seguenti impostazioni sono disponibili per il servizio Remoting.

**Metodo di autenticazione client Flex:** determina il tipo di risposta che il server invia al client quando il servizio richiamato è abilitato per la protezione, l&#39;operazione richiamata non supporta chiamate anonime e il client trasmette credenziali nulle o non valide. Scegliete tra Personalizzato o Base. Il valore predefinito è Base.

**Consenti serializzazione di classi non serializzabili: la** maggior parte degli endpoint AEM moduli consente l&#39;utilizzo di sole classi serializzabili per la chiamata. Nelle versioni precedenti, l&#39;endpoint remoto consentiva l&#39;utilizzo di classi non serializzabili per la chiamata dai client basati su Flex. Per evitare una vulnerabilità di sicurezza descritta in APS11-15, questa è stata modificata. Se si desidera continuare a utilizzare classi non serializzabili con l&#39;endpoint di Flex Remoting, selezionare questa casella di controllo.

## Impostazioni del servizio repository {#repository-service-settings}

Il servizio Repository ( `RepositoryService`) fornisce servizi di archiviazione e gestione delle risorse per AEM moduli. Quando gli sviluppatori creano un&#39;applicazione, possono distribuire le risorse nella directory archivio anziché in un file system. Le risorse possono includere qualsiasi tipo di materiale collaterale, inclusi moduli XML, PDF forms (inclusi  moduli Acrobat), frammenti di modulo, immagini, profili, criteri, file SWF, file DDX, schemi XML, file WSDL e dati di prova.

È possibile utilizzare il repository predefinito incluso nei moduli AEM oppure utilizzare un repository di terze parti (EMC Documentum Content Server, IBM FileNet Content Manager o IBM Content Manager).

Il servizio Provider di repository è un delegato di servizio che funge da interfaccia per un servizio provider. Questo consente di connettersi a un&#39;API comune e non è necessario sapere quale servizio provider sta implementando le funzionalità di storage. Il servizio Provider repository fornisce la memorizzazione del database per le risorse del servizio Repository.

La seguente impostazione è disponibile per il servizio Repository.

**Servizio provider:** il nome del servizio utilizzato come provider di archiviazione. Il valore predefinito è RepositoryProviderService.

## Impostazioni del servizio firma {#signature-service-settings}

Il servizio Firma ( `SignatureService`) consente alla tua organizzazione di proteggere la sicurezza e la privacy  documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che i documenti non vengano alterati. La modifica di un documento ne interrompe la firma. Poiché le funzioni di sicurezza sono applicate al documento stesso, il documento rimane protetto e controllato per l&#39;intero ciclo di vita; oltre il firewall, quando viene scaricato offline e quando viene inviato nuovamente all’organizzazione.

Per il servizio Signature sono disponibili le seguenti impostazioni.

**Nome del servizio SPI HSM remoto:** questa opzione è da utilizzare quando l&#39;HSM è installato su un computer remoto. Specificare questa opzione quando AEM moduli è installato in un Windows a 64 bit e si utilizzano dispositivi HSM per la firma.

**URL del servizio Web HSM remoto:** specificare questa opzione quando AEM moduli viene installato in Windows a 64 bit e si utilizzano dispositivi HSM per la firma.

**Certificazione per includere le modifiche al caricamento del modulo:** quando questa opzione è selezionata, lo stato del modulo XFA viene certificato oltre al modello XFA. Tenere presente che l&#39;attivazione di questa opzione potrebbe avere un impatto negativo sulle prestazioni. Il valore predefinito è true.

**Esegui script JavaScript del documento:** specifica se eseguire gli script JavaScript del documento durante le operazioni di firma. Il valore predefinito è false.

**Elabora documenti con  compatibilità Acrobat 9:** Specifica se abilitare  compatibilità Acrobat 9. Ad esempio, quando questa opzione è selezionata, la certificazione visibile nei PDF dinamici è abilitata. Il valore predefinito è false.

**Incorpora informazioni sulla revoca durante la firma:** Specifica se le informazioni sulla revoca vengono incorporate durante la firma del documento PDF. Il valore predefinito è false.

**Incorpora informazioni di revoca durante la certificazione:** Specifica se le informazioni di revoca vengono incorporate durante la certificazione del documento PDF. Il valore predefinito è false.

**Applica l&#39;incorporazione delle informazioni di revoca per tutti i certificati durante la firma/la certificazione:** Specifica se un&#39;operazione di firma o di certificazione non riesce se non vengono incorporate informazioni di revoca valide per tutti i certificati. Si noti che se un certificato non contiene informazioni CRL o OCSP, viene considerato valido, anche se non vengono recuperate informazioni sulla revoca. Il valore predefinito è false.

**Ordine controllo revoca:** specifica l&#39;ordine del controllo di revoca quando il controllo è possibile tramite i meccanismi Elenco revoca certificati (CRL) e Protocollo di stato del certificato online (OCSP). Il valore predefinito è OCSPFirst.

**Dimensione massima delle informazioni di archiviazione della revoca:** dimensione massima delle informazioni di archiviazione della revoca in kilobyte. AEM moduli tenta di archiviare il maggior numero possibile di informazioni sulla revoca senza superare il limite. Il valore predefinito è 10 KB.

**Supporto di firme create da build preRelease di prodotti di  Adobe:** quando questa opzione è selezionata, la firma creata utilizzando la versione pre-release di  prodotti di Adobe verrà convalidata correttamente. Il valore predefinito è false.

**Opzione Tempo di verifica:** specifica l&#39;ora di verifica del certificato di un firmatario. Il valore predefinito è Proteggi ora corrente.

**Usa informazioni sulla revoca archiviate nella firma durante la convalida:** Specifica se le informazioni sulla revoca archiviate con la firma vengono utilizzate per il controllo della revoca. Il valore predefinito è true.

**Utilizzare le informazioni di convalida memorizzate nel documento per la convalida delle firme:** quando questa opzione è selezionata, le informazioni di convalida (incluse le informazioni di revoca e marca temporale) incorporate nel documento vengono utilizzate per convalidare le firme. Il valore predefinito è true.

**Numero massimo di sessioni di verifica nidificate consentite:** il numero massimo di sessioni di verifica nidificate consentite. AEM moduli utilizza questo valore per evitare un ciclo infinito durante la verifica dei certificati di firma OCSP o CRL quando il certificato OCSP o CRL non è impostato correttamente. Il valore predefinito è 10.

**Massima inclinazione dell&#39;orologio per la verifica:** tempo massimo, in minuti, per il quale il tempo di firma può essere trascorso il tempo di convalida. Se l&#39;inclinazione dell&#39;orologio è maggiore di questo valore, la firma non sarà valida. Il valore predefinito è 65 minuti.

**Cache del ciclo di vita del certificato:** durata di un certificato, recuperato online o con altri metodi, nella cache. Il valore predefinito è 1 giorno.

### Opzioni di trasporto {#transport-options}

**Host proxy:** l&#39;URL dell&#39;host proxy. Utilizzata solo se viene fornito un valore valido. Nessun valore predefinito.

**Porta proxy:** la porta proxy. Digitare un numero di porta valido compreso tra 0 e 65535. Il valore predefinito è 80.

**Nome utente accesso proxy:** il nome utente per l’accesso proxy. Utilizzata solo se viene fornito un valore valido per l&#39;host proxy e la porta proxy. Nessun valore predefinito.

**Password di login proxy:** la password di accesso del proxy. Utilizzata solo se viene fornito un valore valido per l&#39;host proxy, la porta proxy e il nome utente per l&#39;accesso proxy. Nessun valore predefinito.

**Limite massimo di download:** la quantità massima di dati, in MB, che può essere ricevuta per ogni connessione. Il valore minimo è 1 MB e il valore massimo è 1024 MB. Il valore predefinito è 16 MB.

**Tempo di connessione:** tempo massimo di attesa, in secondi, per stabilire una nuova connessione. Il valore minimo è 1 e il valore massimo è 300. Il valore predefinito è 5.

**Tempo di attesa:** tempo massimo di attesa, in secondi, prima che si verifichi un timeout del socket (in attesa del trasferimento dei dati). Il valore minimo è 1 e il valore massimo è 3600. Il valore predefinito è 30.

### Opzioni convalida percorso {#path-validation-options}

**Richiedi criteri espliciti:** specifica se il percorso deve essere valido per almeno uno dei criteri dei certificati associati all&#39;ancoraggio di attendibilità del certificato del firmatario. Il valore predefinito è false.

**Inibisci qualsiasi criterio:** specifica se l&#39;identificatore dell&#39;oggetto criterio (OID) deve essere elaborato se incluso in un certificato. Il valore predefinito è false.

**Disattiva mappatura criteri:** specifica se la mappatura dei criteri è consentita nel percorso di certificazione. Il valore predefinito è false.

**Controlla tutti i percorsi:** specifica se tutti i percorsi devono essere convalidati o se la convalida deve essere interrotta dopo aver trovato il primo percorso valido. Selezionate true o false. Il valore predefinito è false.

**Server LDAP:** il server LDAP utilizzato per cercare i certificati per la convalida del percorso. Nessun valore predefinito.

**Seguire gli URI nell&#39;AIA del certificato:** specifica se gli URI (Uniform Resource Identifier) nell&#39;AIA del certificato vengono elaborati durante l&#39;individuazione del percorso. Il valore predefinito è false.

**Estensione dei vincoli di base richiesta nei certificati CA:** specifica se l&#39;estensione del certificato dei vincoli di base (CA) dell&#39;autorità di certificazione deve essere presente per i certificati CA. Alcuni certificati radice certificati tedeschi iniziali (7 e versioni precedenti) non sono conformi alla RFC 3280 e non contengono l&#39;estensione del vincolo di base. Se è noto che il certificato EE di un utente è concatenato fino a tale radice tedesca, deselezionate questa casella di controllo. Il valore predefinito è true.

**Richiedi firma certificato valida durante la creazione della catena:** specifica se il generatore della catena richiede firme valide sui certificati utilizzati per creare catene. Quando questa casella di controllo è selezionata, il generatore di catene non crea catene con firme RSA non valide sui certificati. Considerare la catena CA > ICA > EE in cui la firma della CA su un&#39;ICA non è valida. Se questa impostazione è vera, la catena si fermerà all&#39;ICA, e la CA non sarà inclusa nella catena. Se questa impostazione è falsa, viene prodotta la catena di 3 certificati completa. Questa impostazione non influisce sulle firme DSA. Il valore predefinito è false.

### Opzioni provider marca temporale {#timestamp-provider-options}

**URL server TSP:** URL del provider di marche temporali predefinito. Utilizzata solo se viene fornito un valore valido. Nessun valore predefinito.

**Nome utente del server TSP:** il nome utente, se richiesto dal provider di marche temporali. Utilizzato solo se per l’URL è stato fornito un valore valido. Nessun valore predefinito.

**Password server TSP:** la password per il nome utente riportato sopra, se richiesta dal provider di marche temporali. Utilizzata solo se per l&#39;URL e il nome utente sono forniti alcuni valori validi. Nessun valore predefinito.

**Algoritmo hash richiesta:** specifica l&#39;algoritmo di hash da utilizzare durante la creazione della richiesta per il provider di marca temporale. Il valore predefinito è SHA1.

**Stile controllo revoca:** specifica lo stile del controllo di revoca utilizzato per determinare lo stato di attendibilità del certificato del provider di marca temporale dal relativo stato di revoca osservato. Il valore predefinito è BestEffort.

**Send Nonce:** Specifica se un nonce viene inviato con la richiesta del provider di marca temporale. Una nonce può essere una marca temporale, un contatore di visite in una pagina Web o un marcatore speciale che abbia lo scopo di limitare o impedire la riproduzione o la riproduzione non autorizzata di un file. Il valore predefinito è true.

**Usa marche temporali scadute durante la convalida:** quando questa opzione è selezionata, è possibile utilizzare marche temporali scadute per recuperare i tempi di convalida delle firme. Il valore predefinito è true.

**Dimensioni di risposta TSP: dimensione** stimata, in byte, della risposta TSP. Questo valore deve rappresentare la dimensione massima della risposta di marca temporale che il provider di marca temporale configurato potrebbe restituire. Non cambiate questo a meno che non siate assolutamente sicuri. Il valore minimo è 60B e il valore massimo è 10240B. Il valore predefinito è 4096B.

**Ignora estensione** server TimeStamp: Selezionare l&#39;opzione  **Ignora** estensione server TimeStamp per arrestare  server AEM Forms dal contattare il server di marca temporale specificato. La selezione di questa opzione consente di evitare errori di processo che si verificano a causa del timeout della connessione tra  server AEM Forms e server di marca temporale.

### Opzioni elenco di revoca certificati {#certificate-revocation-list-options}

**Consulta URI locale:** prima: specifica se la posizione CRL fornita in URI locale o ricerca CRL deve avere la preferenza su qualsiasi posizione specificata all&#39;interno di un certificato ai fini del controllo della revoca. Il valore predefinito è false.

**URI locale per ricerca CRL:** URL del provider CRL locale. Questo valore viene consultato solo se l&#39;impostazione Consulta URI locale Primo è impostata su true. Nessun valore predefinito.

**Stile controllo revoca:** specifica lo stile del controllo di revoca utilizzato per determinare lo stato di attendibilità del certificato del provider CRL dal relativo stato di revoca osservato. Il valore predefinito è BestEffort.

**Server LDAP per ricerca CRL:** il server LDAP utilizzato per ottenere i CRL (come www.ldap.com). Tutte le query basate su DN per i CRL verranno indirizzate a questo server. Nessun valore predefinito.

**Vai online:** specifica se andare online per recuperare un CRL. Se false, vengono consultati solo i CRL memorizzati nella cache (su disco locale o incorporati con firma). Il valore predefinito è true.

**Ignora date validità:** specifica se ignorare i tempi di aggiornamento e aggiornamento successivi della risposta, impedendo a questi tempi di avere un effetto negativo sulla validità della risposta. Il valore predefinito è false.

**Richiedi estensione AKI in CRL:** specifica se l&#39;estensione ID chiave autorità deve essere inclusa in un CRL. Il valore predefinito è false.

### Opzioni del protocollo di stato del certificato online {#online-certificate-status-protocol-options}

**URL server OCSP:** URL per il server OCSP predefinito. L&#39;utilizzo del server OCSP specificato tramite questo URL dipende dall&#39;impostazione dell&#39;opzione URL a consultazione. Nessun valore predefinito.

**Opzione URL per consultare:** controlla l&#39;elenco e l&#39;ordine dei server OCSP utilizzati per eseguire il controllo dello stato. Il valore predefinito è UseAIAInCert.

**Stile controllo revoca:** specifica lo stile del controllo di revoca utilizzato per verificare il certificato del server OCSP. Il valore predefinito è CheckIfAvailable.

**Send Nonce:** Specifica se un collegamento viene inviato con la richiesta OCSP. Una nonce può essere una marca temporale, un contatore di visite in una pagina Web o un marcatore speciale che abbia lo scopo di limitare o impedire la riproduzione o la riproduzione non autorizzata di un file. Il valore predefinito è true.

**Tempo massimo di inclinazione dell&#39;orologio:** inclinazione massima consentita, in minuti, tra il tempo di risposta e l&#39;ora locale. Il valore minimo è 0 e il valore massimo è 2147483647m. Il valore predefinito è 5m.

**Tempo di freshness risposta: tempo** massimo, in minuti, per il quale una risposta OCSP precostruita è considerata valida. Il valore minimo è 1m e il valore massimo consentito è 2147483647. Il valore predefinito è 525600 (un anno).

**Firma richiesta OCSP:** specifica se la richiesta OCSP deve essere firmata. Il valore predefinito è false.

**Alias credenziali firmatario richiesta:** specifica l&#39;alias credenziale da utilizzare per la firma della richiesta OCSP se la firma è abilitata. Utilizzata solo se la firma della richiesta OCSP è abilitata. Nessun valore predefinito.

**Vai online:** specifica se andare online per eseguire il controllo delle revoche. Il valore predefinito è true.

**Ignora i tempi thisUpdate e nextUpdate della risposta:** Specifica se ignorare i tempi di aggiornamento e aggiornamento successivo della risposta, impedendo a questi tempi di avere un effetto negativo sulla validità della risposta. Il valore predefinito è false.

**Consenti estensione OCSPNoCheck:** specifica se l&#39;estensione OCSPNoCheck è consentita nel certificato di firma della risposta. Il valore predefinito è true.

**Richiedi OCSP ISIS-MTT CertHash Extension:** Specifica se nelle risposte OCSP deve essere inclusa un&#39;estensione hash della chiave pubblica del certificato. Il valore predefinito è false.

### Opzioni di gestione errori per il debug {#error-handling-options-for-debugging}

**Elimina cache certificati nella successiva chiamata API:** specifica se rimuovere la cache certificati quando viene chiamata la successiva operazione del servizio firma. Dopo aver chiamato l&#39;operazione, questa opzione viene reimpostata su false. Il valore predefinito è false.

**Elimina cache CRL dalla chiamata API successiva:** specifica se rimuovere la cache CRL quando viene chiamata la successiva operazione del servizio firma. Dopo aver chiamato l&#39;operazione, questa opzione viene reimpostata su false. Il valore predefinito è false.

**Elimina cache OCSP dalla successiva chiamata API:** Specifica se rimuovere la cache OCSP quando viene chiamata la successiva operazione del servizio firma. Dopo aver chiamato l&#39;operazione, questa opzione viene reimpostata su false. Il valore predefinito è false.

## Impostazioni del servizio Cartelle esaminate {#watched-folder-service-settings}

Il servizio Cartelle esaminate ( `WatchedFolder`) configura gli attributi comuni per tutti gli endpoint delle cartelle esaminate. Fornisce inoltre valori predefiniti per gli endpoint delle cartelle esaminate. (vedere [Configurazione degli endpoint delle cartelle esaminate](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).) Non viene richiamato da applicazioni client esterne né utilizzato nei processi creati in Workbench.

Per il servizio Cartella esaminata sono disponibili le seguenti impostazioni.

**Espressione cron:** l&#39;espressione cron utilizzata dal quarzo per pianificare il polling della directory di input.

**Ripeti conteggio:** il numero di volte in cui viene effettuato il polling della directory di input. Conteggio ripetizioni predefinito da utilizzare se questo valore non è specificato nella configurazione dell&#39;endpoint. Il valore -1 indica la scansione indefinita della directory. Il valore predefinito è -1.

**Intervallo ripetizione:** il numero predefinito, se in secondi, tra ciascun sondaggio. Questo valore viene utilizzato come intervallo di ripetizione, a meno che non venga specificato un valore diverso nella configurazione dell’endpoint della cartella controllata. Il valore predefinito è 5. Per ulteriori informazioni, consultate la descrizione dell&#39;impostazione Dimensione batch.

**Asincrono:** identifica il tipo di chiamata come asincrono o sincrono. I processi transitori e sincroni possono essere invocati solo in modo sincrono. Il valore predefinito è asincrono.

**Tempo di attesa:** il valore predefinito per il tempo, in secondi, dopo il quale i file vengono recuperati dalle cartelle di input. Se il file o la cartella è più vecchia del tempo specificato nel tempo di attesa, viene prelevata per l’elaborazione. Il valore predefinito è 0.

**Dimensione batch:** il valore predefinito per il numero di file o cartelle elaborati per scansione. Il valore predefinito è 2.

Le impostazioni Intervallo di ripetizione e Dimensione batch determinano quanti file vengono raccolti da Cartella esaminata in ogni scansione. Cartella esaminata utilizza un pool di thread Quartz per eseguire la scansione della cartella di input. Il pool di thread è condiviso con altri servizi. Se l’intervallo di scansione è ridotto, i thread eseguono spesso la scansione della cartella di input. Se i file vengono rilasciati frequentemente nella cartella esaminata, tenete l’intervallo di scansione ridotto. Se i file vengono omessi raramente, usate un intervallo di scansione maggiore in modo che gli altri servizi possano usare i thread.

Se un grande volume di file viene eliminato, ingrandire la dimensione del batch. Ad esempio, se il servizio richiamato dall’endpoint delle cartelle esaminate può elaborare 700 file al minuto e gli utenti rilasciano i file nella cartella di input allo stesso ritmo, impostando quindi la dimensione batch su 350 e l’intervallo di ripetizione su 30 secondi sarà più facile per le prestazioni delle cartelle esaminate senza dover sostenere troppo spesso il costo di scansione della cartella esaminata.

Quando i file vengono rilasciati nella cartella esaminata, elenca i file nell&#39;input, il che può ridurre le prestazioni se la scansione avviene ogni secondo. Aumentare l&#39;intervallo di scansione può migliorare le prestazioni. Se il volume di file rilasciato è piccolo, regolare le dimensioni del batch e l&#39;intervallo di ripetizione di conseguenza. Ad esempio, se 10 file vengono eliminati ogni secondo, provate a impostare l’intervallo di ripetizione su 1 secondo e la dimensione del batch su 10.

In una configurazione cluster, la dimensione batch per l’endpoint di una cartella controllata non viene ridimensionata in più nodi del cluster. Ad esempio, se la dimensione del batch è impostata su `2` per un cluster a due nodi e l&#39;opzione Limita è selezionata, i nodi elaborano i file collettivamente in batch di due anziché ciascun nodo elaborando due file alla volta.

**Sovrascrivi nomi file duplicati:** Una stringa booleana che specifica se la cartella esaminata sovrascrive i nomi dei file di risultati duplicati e se sovrascrivere i documenti conservati con lo stesso nome.

**Mantieni cartella:** il valore predefinito per la cartella preserve. Questa cartella viene utilizzata per copiare i file sorgente in caso di riuscita dell’elaborazione dell’input. Questo valore può essere un percorso vuoto, relativo o assoluto con un pattern di file come descritto per l&#39;impostazione Cartella risultati.

**Cartella degli errori:** il nome della cartella in cui vengono copiati i file degli errori. Questo valore può essere un percorso vuoto, relativo o assoluto con un pattern di file come descritto per l&#39;impostazione Cartella risultati.

**Cartella risultati:** nome predefinito per la cartella dei risultati. Questa cartella viene utilizzata per copiare i file dei risultati. Questo valore può essere un percorso vuoto, relativo o assoluto con il seguente pattern di file.

* %F = prefisso del nome del file
* %E = estensione del nome del file
* %Y = anno (completo)
* %y = anno (ultime due cifre)
* %M = mese
* %D = giorno del mese
* %d = giorno dell&#39;anno
* %H = ora (24 ore)
* %h = ora (orologio da 12 ore)
* %m = minuto
* %s = secondo
* %l = millisecondi
* %R = numero casuale (da 0 a 9)
* %P = ID processo o processo

Ad esempio, se il valore è alle 20 del 17 luglio 2009 e si specifica `C:/Test/WF0/failure/%Y/%M/%D/%H/`, la cartella dei risultati è `C:/Test/WF0/failure/2009/07/17/20`.

Se il percorso non è assoluto ma relativo, la cartella viene creata all’interno della cartella esaminata. Per ulteriori informazioni sui pattern di file, vedere [Informazioni sui pattern di file](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Più piccole sono le dimensioni delle cartelle dei risultati, migliori saranno le prestazioni delle cartelle esaminate. Ad esempio, se il carico stimato per la cartella esaminata è di 1000 file ogni ora, provate a creare un pattern come `result/%Y%M%D%H` in modo che venga creata una nuova sottocartella ogni ora. Se il carico è minore (ad esempio, 1000 file al giorno), è possibile utilizzare un pattern come `result/%Y%M%D`.

**Cartella stage:** il nome predefinito per la cartella dell’area di visualizzazione all’interno della cartella esaminata.

**Cartella di input:** il nome predefinito per la cartella di input all’interno della cartella esaminata.

**Mantieni in caso di errore:** se true, i file originali vengono conservati nella cartella degli errori in caso di errore.

**Limitazione:** quando questa opzione è selezionata, limita il numero di processi di cartelle controllati che AEM i moduli vengono elaborati in un dato momento. Il valore Dimensione batch determina il numero massimo di processi (vedere Informazioni sulla limitazione).

## Impostazioni servizio Web {#web-service-service-settings}

Il servizio Web Service ( `WebService`) consente ai processi di richiamare le operazioni del servizio Web.

Il servizio Web consente ai processi di richiamare le operazioni del servizio Web. Ad esempio, un&#39;organizzazione potrebbe desiderare di integrare un processo per memorizzare e recuperare informazioni quali i dettagli dei contatti e degli account richiamando i servizi Web esposti di un fornitore di servizi. Il servizio Web richiama un servizio Web specificato e trasmette i valori per ciascuno dei suoi parametri. quindi salva i valori restituiti dall&#39;operazione in una variabile designata all&#39;interno di un processo.

Il servizio Web Service interagisce con i servizi Web inviando e ricevendo messaggi SOAP. Il servizio supporta inoltre l&#39;invio di allegati MIME, MTOM e SwaRef con messaggi SOAP utilizzando il protocollo WS-Attachment. Le interazioni del servizio Web sono compatibili con i sistemi SAP e i servizi Web .NET.

Per il servizio Web Service sono disponibili le seguenti impostazioni.

**Archivio chiavi:** percorso completo del file dell&#39;archivio chiavi che contiene la chiave privata da utilizzare per l&#39;autenticazione. Il server moduli deve essere in grado di accedere al file.

**Password archivio chiavi:** la password per il file dell&#39;archivio chiavi.

**Tipo archivio chiavi:** il tipo di archivio chiavi. Non specificare alcun valore per utilizzare il tipo di keystore predefinito configurato per la JVM che esegue il server dei moduli. In caso contrario, specificare uno dei seguenti valori:

* jks
* pkcs12
* cms
* stupidaggini

**Trust Store:** percorso completo del file dell&#39;archivio di trust che contiene la chiave pubblica del server del servizio Web.

**Password archivio attendibili:** la password per il file truststore.

**Tipo archivio attendibili:** il tipo di archivio attendibili. Non specificare alcun valore per utilizzare il tipo di keystore predefinito configurato per la JVM che esegue il server dei moduli. In caso contrario, specificare uno dei seguenti valori:

* jks
* pkcs12
* cms
* stupidaggini

## Impostazioni del servizio Trasformazione XSLT {#xslt-transformation-service-settings}

Il servizio Trasformazione XSLT ( `XSLTService`) consente ai processi di applicare le trasformazioni XSLT (Extensible Stylesheet Language Transformations) sui documenti XML.

Per il servizio Trasformazione XSLT è disponibile la seguente impostazione.

**Nome fabbrica:** il nome completo della classe Java da utilizzare per eseguire le trasformazioni XSLT. Se non viene specificato alcun valore, viene utilizzata la fabbrica predefinita configurata in Java Virtual Machine che esegue il server dei moduli.

## Modifica delle impostazioni di protezione per un servizio {#modifying-security-settings-for-a-service}

il server dei moduli consente di configurare le impostazioni di protezione per ogni servizio, configurando così un controllo di accesso dettagliato a livello di singolo servizio.

Sono installati profili di protezione predefiniti che possono essere configurati in base alle esigenze del sistema. A ciascun profilo di protezione è associato un dominio e viene creato a livello di utente o di gruppo.

### Modifica delle impostazioni di protezione per un servizio {#modify-security-settings-for-a-service}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Nella pagina Gestione dei servizi, fate clic sul servizio da configurare.
1. Fate clic sulla scheda Protezione.
1. Nell&#39;elenco Richiedi ai chiamanti di autenticare, selezionare Sì o No per specificare se il servizio può essere invocato con o senza le credenziali.

   Se si seleziona Sì, il chiamante del servizio deve essere autenticato e l&#39;entità utente per quel chiamante deve essere autorizzata a richiamare il servizio; in caso contrario, il tentativo di chiamata verrà rifiutato.

   Se si seleziona No, il chiamante del servizio potrebbe essere autenticato o meno. L&#39;invocazione del servizio avrà sempre esito positivo perché non è presente alcun controllo di autorizzazione.

1. Per i servizi che contengono una o più operazioni contrassegnate per l&#39;accesso anonimo, selezionare o deselezionare Accesso anonimo consentito. Quando l&#39;accesso anonimo è abilitato, qualsiasi utente all&#39;interno del sistema può richiamare le operazioni sul servizio. Se l&#39;accesso anonimo è disattivato, agli utenti deve essere concessa l&#39;autorizzazione per chiamare il servizio e richiamare le operazioni. Agli utenti vengono concesse queste autorizzazioni direttamente o come parte di un gruppo che dispone di tali autorizzazioni.
1. Per alcuni servizi, l&#39;account utente che esegue l&#39;operazione influisce sui risultati. Ad esempio, in Content Services (Obsoleto), l&#39;utente che memorizza il contenuto è il proprietario del contenuto, il che influisce su chi può accedere successivamente al contenuto. Se si utilizza un processo per memorizzare il contenuto, è necessario considerare l&#39;utente utilizzato per eseguire il servizio Document Management, in quanto tale utente sarà proprietario del contenuto memorizzato.

   Per specificare l&#39;identità di esecuzione utilizzata da un servizio per eseguire le operazioni, selezionare Specifica esecuzione con nome, selezionare un&#39;opzione dall&#39;elenco associato, quindi fare clic su Salva. Scegliete tra le seguenti opzioni:

   **Invoker:** utilizza la stessa identità dell&#39;utente che ha richiamato il servizio.

   **Sistema:** utilizza l&#39;utente di sistema per eseguire il servizio con privilegi completi.

   **Utente denominato:** consente di eseguire il servizio come utente specifico. Quando selezionate questa opzione, fate clic su Seleziona utente per visualizzare la pagina Seleziona principale, in cui potete cercare e selezionare l&#39;utente.

   Se non si seleziona Specifica esecuzione con nome, viene utilizzato il comportamento predefinito.

   >[!NOTE]
   >
   >I servizi di rendering e invio utilizzati con le variabili xfaForm, Document Form e Form vengono sempre eseguiti utilizzando l&#39;account utente di sistema.

1. Fate clic su Aggiungi entità per specificare le autorizzazioni di cui dispongono utenti e gruppi per questo servizio.
1. Nella schermata Seleziona entità sono visualizzati gli utenti e i gruppi configurati in Gestione utente. Se l’utente o il gruppo desiderato non è visualizzato, utilizzate la funzione di ricerca per individuarlo. Fate clic sul nome di un utente o di un gruppo.
1. Nella schermata Aggiungi autorizzazioni, selezionate le autorizzazioni da assegnare all’utente o al gruppo per questo servizio:

   * **INVOKE_PERM:** Richiamare tutte le operazioni sul servizio
   * **MODIFY_CONFIG_PERM:** Per modificare la configurazione di un servizio
   * **SUPERVISOR_PERM:** Per visualizzare i dati dell&#39;istanza di processo per un servizio creato da un processo
   * **START_STOP_PERM:** Per avviare e arrestare un servizio
   * **ADD_REMOVE_ENDPOINTS_PERM:** Aggiunta, rimozione e modifica di endpoint per un servizio
   * **CREATE_VERSION_PERM:** Per creare una nuova versione del servizio
   * **DELETE_VERSION_PERM:** Per eliminare una versione del servizio
   * **MODIFY_VERSION_PERM:** Per modificare una versione del servizio
   * **READ_PERM:** Visualizzazione del servizio
   * **PROCESS_OWNER_PERM:** da utilizzare in una versione futura dei moduli AEM. Non utilizzare questa autorizzazione.
   * **SERVICE_MANAGER_PERM:** da utilizzare in una versione futura dei moduli AEM. Non utilizzare questa autorizzazione.
   * **SERVICE_AGENT_PERM:** da utilizzare in una versione futura dei moduli AEM. Non utilizzare questa autorizzazione.

1. Fate clic su Aggiungi.

### Rimuovere l&#39;entità da un profilo di sicurezza {#remove-the-principal-from-a-security-profile}

1. Nella pagina Gestione dei servizi, selezionate il servizio da configurare.
1. Fare clic sulla scheda **Protezione**, selezionare il profilo di protezione da rimuovere, quindi fare clic su **Rimuovi**.

## Configurazione del pool per un servizio {#configuring-pooling-for-a-service}

Ogni servizio può sfruttare le funzionalità di pooling per gestire le richieste di chiamata in arrivo. L&#39;utilizzo di un pool di servizi garantisce che le istanze del servizio vengano richiamate da un singolo thread alla volta e riutilizzate tra le richieste di chiamata, il che potrebbe migliorare le prestazioni. Potete inoltre utilizzare il pool per specificare l&#39;opzione Massimo istanze di servizio asincrone, che consente ai servizi di limitare il numero di richieste gestite in parallelo.

### Abilita pooling {#enable-pooling}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Nella pagina Gestione dei servizi, fate clic sul servizio da configurare.
1. Fate clic sulla scheda Pool.
1. Nell&#39;elenco Strategia elaborazione richieste, selezionare Istanze in pool per tutte le richieste.
1. Nella casella Dimensione pool di istanze del servizio iniziale, immettere la dimensione iniziale del pool. Quando il servizio viene distribuito, questo numero viene utilizzato per determinare il numero di istanze di implementazione del servizio create e allocate al pool gratuito, in attesa delle richieste di chiamata. Questo consente al contenitore del servizio di rispondere immediatamente alle richieste di chiamata senza dover prima inizializzare un&#39;istanza del servizio.
1. Nella casella Dimensione massima pool di istanze del servizio, immettere il numero massimo di istanze nel pool per un determinato servizio. Questa impostazione controlla il numero di thread che possono eseguire un determinato servizio in un dato momento. Il valore predefinito è 0, che restituisce una dimensione illimitata del pool.
1. Nella casella Istanze di servizio asincrone massime, immettere il numero massimo di istanze del pool che possono essere utilizzate per il servizio delle richieste asincrone in un dato momento. Questa impostazione consente al servizio di limitare il numero di richieste che può gestire in parallelo.
1. Nella casella Timeout attesa chiamata, specificare il numero di millisecondi per l&#39;attesa che un servizio diventi disponibile per una richiesta di chiamata. Se non si specifica un valore per questa impostazione, il valore predefinito è 0, che non genera tempi di attesa.
1. Fate clic su Salva.

### Rimuovi pooling {#remove-pooling}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Nella pagina Gestione dei servizi, fate clic sul servizio da configurare.
1. Fate clic sulla scheda Pool.
1. Nell&#39;elenco Strategia elaborazione richieste, selezionare Nuova istanza per ogni richiesta o Singola istanza per tutte le richieste.

   **Istanza singola per tutte le richieste:** Un&#39;istanza del servizio viene creata e memorizzata nella cache quando la prima richiesta viene inoltrata nel contenitore. Ogni richiesta successiva utilizza la stessa istanza del servizio per gestire la richiesta.

   **Nuova istanza per ogni richiesta:** viene creata una nuova istanza del servizio per ogni chiamata ricevuta.

1. Fate clic su Salva.

