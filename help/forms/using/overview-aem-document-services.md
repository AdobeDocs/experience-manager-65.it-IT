---
title: Panoramica di AEM Document Services
seo-title: Panoramica di AEM Document Services
description: AEM Document Services è un set di servizi OSGi per la creazione, l'assemblaggio e la protezione di documenti PDF.
seo-description: AEM Document Services è un set di servizi OSGi per la creazione, l'assemblaggio e la protezione di documenti PDF.
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 0%

---


# Panoramica di AEM Document Services{#overview-of-aem-document-services}

AEM Document Services è un set di servizi OSGi per la creazione, l&#39;assemblaggio e la protezione di documenti PDF. Document Services contiene i seguenti servizi:

## Servizio di output {#output-service}

Il servizio Output consente di creare documenti in diversi formati, tra cui PDF, formati per stampanti laser e formati per stampanti di etichette. I formati delle stampanti laser sono PostScript e PCL (Printer Control Language). L&#39;elenco seguente specifica i formati di stampa delle etichette:

* Zebra (ZPL)
* Intermec (IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

È possibile inviare un documento a una stampante di rete, a una stampante locale o a un file nel file system. Il servizio Output unisce i dati del modulo XML a una struttura del modulo per generare un documento. Il servizio Output può generare un documento senza unire i dati del modulo XML al documento. Tuttavia, il flusso di lavoro principale consiste nell&#39;unione dei dati nel documento.

>[!NOTE]
>
>Una struttura del modulo viene in genere creata utilizzando Designer. Per informazioni sulla creazione di strutture del modulo per il servizio Output, vedere la Guida di Designer.

Quando si utilizza il servizio Output per unire i dati XML a una struttura del modulo, si ottiene un documento PDF non interattivo. Un documento PDF non interattivo non consente agli utenti di immettere dati nei relativi campi. Al contrario, è possibile utilizzare il servizio Forms per creare un modulo PDF interattivo che consenta agli utenti di immettere i dati nei campi.

Sono disponibili per l&#39;uso le quattro seguenti operazioni del servizio Output:

* **generatePDFOuput**: Unisce una struttura del modulo ai dati per generare un documento PDF
* **generatePrintedOutput**: Unisce una struttura del modulo ai dati del modulo per generare un documento da inviare a una stampante laser o di rete label

* **generatePDFOutputBatch**: Unisce più modelli con più record di dati in una singola chiamata per generare un batch di file PDF. È inoltre possibile generare un singolo PDF combinando tutti i PDF
* **generatePrintedOutputBatch**: Unisce più modelli con più record di dati in una singola chiamata per generare un batch di documenti di stampa (PS,PCL,ZPL,DPL,IPL,TPCL). È inoltre possibile generare un singolo documento di stampa.

## Servizio assemblatore {#assembler-service}

Il servizio Assembler consente di combinare, ridisporre e integrare documenti PDF e XDP e di ottenere informazioni sui documenti PDF. Ogni processo inviato al servizio Assembler include un documento DDX (Document Description XML), documenti di origine e risorse esterne (stringhe e grafica). Il documento DDX fornisce istruzioni su come utilizzare i documenti di origine per produrre un insieme di documenti risultanti.

Oltre alle funzionalità di cui sopra, il servizio Assembler:

* Converte i documenti PDF in PDF/A standard.
* Trasforma PDF forms, moduli XML (creati in Designer) e PDF forms (creati in  Acrobat) in PDF/A-1b, PDF/A-2b e PDFA/A-3b.
* Converte i documenti PDF firmati o non firmati (sono necessarie le firme digitali).
* Convalida la conformità di un file PDF/A e lo converte, se necessario.

### Informazioni su DDX {#about-ddx}

Quando si utilizza il servizio Assembler, utilizzare un linguaggio XML denominato Document Description XML (DDX) per descrivere l&#39;output desiderato. DDX è un linguaggio di markup dichiarativo i cui elementi rappresentano blocchi costitutivi di documenti. Tali blocchi costitutivi includono documenti PDF, documenti XDP, frammenti di modulo XDP e altri elementi quali commenti, segnalibri e testo formattato.

Il documento DDX può specificare i documenti risultanti con le seguenti caratteristiche:

* Documento PDF assemblato da più documenti PDF
* Più documenti PDF suddivisi in un singolo documento PDF
* PORTFOLIO PDF che include un&#39;interfaccia utente indipendente e più documenti PDF e non PDF
* Documento XDP assemblato da più documenti XDP
* Documento XDP contenente frammenti XML inseriti in modo dinamico in un documento XDP
* Documento PDF che crea un pacchetto per un documento XDP
* File XML che generano rapporti sulle caratteristiche di un documento PDF. Le caratteristiche riportate includono testo, commenti, dati del modulo, allegati di file, file utilizzati in Portfoli PDF, segnalibri e proprietà PDF. Le proprietà PDF includono le proprietà del modulo, la rotazione della pagina e l&#39;autore del documento.

È possibile utilizzare DDX per espandere i documenti PDF come parte dell&#39;assemblaggio o dello smontaggio del documento. Potete specificare una combinazione qualsiasi dei seguenti effetti:

* Aggiungere o rimuovere filigrane o sfondi sulle pagine selezionate.
* Aggiungere o rimuovere intestazioni e piè di pagina sulle pagine selezionate.
* Rimuove la struttura e le capacità di navigazione di un pacchetto PDF o di un Portfolio PDF. Il risultato è un singolo file PDF.
* Rinumerare le etichette di pagina. Le etichette delle pagine vengono in genere utilizzate per la numerazione delle pagine.
* Importare metadati da un altro documento sorgente.
* Aggiungere o rimuovere allegati di file, segnalibri, collegamenti, commenti e JavaScript.
* Impostate le caratteristiche di visualizzazione iniziali e ottimizzate per la visualizzazione sul Web.
* Impostare le autorizzazioni per i PDF crittografati.
* Ruotare le pagine o ruotare e spostare il contenuto sulle pagine.
* Modificare le dimensioni delle pagine selezionate.
* Unione di dati con un PDF basato su XFA.

È possibile utilizzare una semplice mappa di input per specificare le posizioni dei documenti sorgente e risultanti. È inoltre possibile utilizzare i seguenti tipi di URL dati esterni:

* File
* FTP
* HTTP/HTTPS

## Servizio di assicurazione documenti {#doc-assurance-service}

Doc Assurance Service consente di cifrare e decrittografare i documenti, ampliare le funzionalità di  Adobe Reader con diritti di utilizzo aggiuntivi e aggiungere firme digitali ai documenti. Gli utenti possono interagire facilmente con PDF forms e documenti, migliorando al contempo la sicurezza, l&#39;archiviazione e la conformità.

Il servizio Doc Assurance contiene tre servizi: firma, cifratura e estensione del lettore.

### Servizio firma {#signature-service}

Il servizio Signature consente di utilizzare firme digitali e documenti sul server AEM. Ad esempio, il servizio Signature è in genere utilizzato nelle situazioni seguenti:

* Il server AEM certifica un modulo prima che venga inviato all&#39;utente per l&#39;apertura, utilizzando  Acrobat o  Adobe Reader.
* Il server AEM convalida una firma aggiunta a un modulo utilizzando  Acrobat o  Adobe Reader.
* Il server AEM firma un modulo per conto di un notaio pubblico.

Il servizio Firma accede ai certificati e alle credenziali memorizzate nell&#39;archivio certificati attendibili.

### Servizio di crittografia {#encryption-service}

Il servizio di cifratura consente di cifrare e decrittografare i documenti. Quando un documento viene crittografato, il relativo contenuto diventa illeggibile. È possibile cifrare l&#39;intero documento PDF (inclusi contenuto, metadati e allegati), qualsiasi altro elemento oltre ai metadati, o solo gli allegati. Un utente autorizzato può decifrare il documento per ottenere l&#39;accesso ai contenuti. Se un documento PDF è crittografato con una password, l&#39;utente deve specificare la password aperta per poter visualizzare il documento in  Adobe Reader o  Acrobat. Se un documento PDF è crittografato con un certificato, l&#39;utente deve decrittografare il documento PDF con una chiave privata (certificato). La chiave privata utilizzata per decifrare il documento PDF deve corrispondere alla chiave pubblica utilizzata per cifrarlo.

### Servizio estensione Reader {#reader-extension-service}

Il servizio Estensioni di Reader consente alla vostra azienda di condividere facilmente documenti PDF interattivi estendendo le funzionalità di  Adobe Reader con diritti di utilizzo aggiuntivi. Il servizio Estensioni Reader funziona con  Adobe Reader 7.0 o versione successiva. Il servizio aggiunge diritti di utilizzo a un documento PDF. Questa azione attiva le funzioni solitamente non disponibili all&#39;apertura di un documento PDF tramite  Adobe Reader, ad esempio l&#39;aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento. Gli utenti di terze parti non richiedono software o plug-in aggiuntivi per lavorare con documenti abilitati per i diritti.

Quando ai documenti PDF vengono aggiunti i diritti di utilizzo appropriati, i destinatari possono eseguire le seguenti attività direttamente da  Adobe Reader:

* Compilare documenti e moduli PDF online o offline, consentendo ai destinatari di salvare le copie localmente per i propri record e mantenendo intatte le informazioni aggiunte
* Salvare i documenti PDF su un disco rigido locale per conservare il documento originale ed eventuali commenti, dati o allegati aggiuntivi
* Allegare file e clip multimediali a documenti PDF
* Firmare, certificare e autenticare i documenti PDF applicando firme digitali mediante tecnologie PKI (Public Key Infrastructure) standard di settore
* Invio elettronico di documenti PDF completati o annotati
* Utilizzo di documenti e moduli PDF come front-end di sviluppo intuitivo per database e servizi Web interni
* Condividere documenti PDF con altri utenti in modo che i revisori possano aggiungere commenti utilizzando strumenti di marcatura intuitivi. Questi strumenti includono note elettroniche, timbri, evidenziazioni e barratura del testo. Le stesse funzioni sono disponibili in  Acrobat.
* Supporto della decodifica di moduli con codice a barre.

Queste speciali funzionalità utente vengono attivate automaticamente quando un documento PDF con diritti viene aperto in  Adobe Reader. Quando l&#39;utente ha finito di lavorare con un documento con diritti, tali funzioni vengono nuovamente disattivate in  Adobe Reader. Rimangono disabilitate finché l&#39;utente non riceve un altro documento PDF con diritti.

Il servizio DocAssurance non è disponibile per l&#39;uso. Per configurare il servizio DocAssurance, vedere [Installazione e configurazione di Document Services](../../forms/using/install-configure-document-services.md).

## Invia a servizio stampante {#send-to-printer-service}

Invia a servizio stampante fornisce l&#39;API per l&#39;invio di documenti a una stampante specificata per la stampa.
