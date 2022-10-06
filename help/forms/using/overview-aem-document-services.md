---
title: Panoramica di AEM Document Services
seo-title: Overview of AEM Document Services
description: AEM Document Services è un set di OSGi Services per la creazione, l’assemblaggio e la protezione dei documenti PDF.
seo-description: AEM Document Services are a set of OSGi Services for creating, assembling, and securing PDF Documents.
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# Panoramica di AEM Document Services{#overview-of-aem-document-services}

AEM Document Services è un set di OSGi Services per la creazione, l’assemblaggio e la protezione dei documenti PDF. Document Services contiene i seguenti servizi:

## Servizio di output {#output-service}

Il servizio Output consente di creare documenti in diversi formati, tra cui PDF, formati di stampa laser e formati di stampa delle etichette. I formati della stampante laser sono PostScript e PCL (Printer Control Language). L&#39;elenco seguente specifica i formati di stampa delle etichette:

* Zebra (ZPL)
* Intermec (IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

È possibile inviare un documento a una stampante di rete, a una stampante locale o a un file nel file system. Il servizio Output unisce i dati del modulo XML a una struttura del modulo per generare un documento. Il servizio Output può generare un documento senza unire i dati del modulo XML al documento. Tuttavia, il flusso di lavoro principale sta unendo i dati nel documento.

>[!NOTE]
>
>Una struttura del modulo viene in genere creata utilizzando Designer. Per informazioni sulla creazione di strutture del modulo per il servizio Output, vedere la Guida di Designer.

Quando si utilizza il servizio Output per unire i dati XML a una struttura del modulo, si ottiene un documento PDF non interattivo. Un documento PDF non interattivo non consente agli utenti di immettere dati nei campi. È invece possibile utilizzare il servizio Forms per creare un modulo PDF interattivo che consenta agli utenti di immettere i dati nei campi corrispondenti.

Sono disponibili per l&#39;uso le seguenti quattro operazioni del servizio di output:

* **generatePDFOuput**: Unisce una struttura del modulo ai dati per generare un documento PDF
* **generatePrintOutput**: Unisce una struttura del modulo ai dati del modulo per generare un documento da inviare a una stampante laser o a una stampante di rete per etichette

* **generatePDFOutputBatch**: Unisce più modelli con più record di dati in una singola chiamata per generare un batch di file PDF. È inoltre possibile generare un singolo PDF combinando tutti i PDF
* **generatePrintOutputBatch**: Unisce più modelli con più record di dati in una singola chiamata per generare un batch di documenti di stampa (PS,PCL,ZPL,DPL,IPL,TPCL). È inoltre possibile generare un singolo documento di stampa.

## Servizio assemblatore {#assembler-service}

Il servizio Assembler consente di combinare, ridisporre e integrare documenti PDF e XDP e di ottenere informazioni sui documenti PDF. Ogni processo inviato al servizio Assembler include un documento Document Description XML (DDX), documenti di origine e risorse esterne (stringhe e grafica). Il documento DDX fornisce istruzioni su come utilizzare i documenti di origine per produrre un set di documenti risultanti.

Oltre alle funzionalità di cui sopra, il servizio Assembler:

* Converte i documenti PDF in standard PDF/A.
* Trasforma PDF forms, moduli XML (creati in Designer) e PDF forms (creati in Acrobat) in PDF/A-1b, PDF/A-2b e PDFA/A-3b.
* Converte i documenti PDF firmati o non firmati (sono richieste le firme digitali).
* Convalida la conformità di un file PDF/A e lo converte se necessario.

### Informazioni su DDX {#about-ddx}

Quando si utilizza il servizio Assembler, utilizzare un linguaggio basato su XML denominato Document Description XML (DDX) per descrivere l&#39;output desiderato. DDX è un linguaggio di markup dichiarativo i cui elementi rappresentano blocchi predefiniti di documenti. Questi blocchi predefiniti includono documenti PDF, documenti XDP, frammenti di modulo XDP e altri elementi come commenti, segnalibri e testo con stili.

Il documento DDX può specificare i documenti risultanti con le seguenti caratteristiche:

* Documento PDF assemblato da più documenti PDF
* Più documenti PDF suddivisi in un singolo documento PDF
* Portfolio PDF che include un’interfaccia utente indipendente e più documenti PDF e non PDF
* Documento XDP assemblato da più documenti XDP
* Documento XDP contenente frammenti XML inseriti in modo dinamico in un documento XDP
* Documento PDF che crea un pacchetto per un documento XDP
* File XML che generano rapporti sulle caratteristiche di un documento PDF. Le caratteristiche segnalate includono testo, commenti, dati del modulo, allegati di file, file utilizzati nei Portfoli PDF, segnalibri e proprietà di PDF. Le proprietà di PDF includono le proprietà del modulo, la rotazione della pagina e l’autore del documento.

È possibile utilizzare DDX per integrare i documenti PDF come parte dell&#39;assemblaggio o dello smontaggio dei documenti. È possibile specificare una combinazione dei seguenti effetti:

* Aggiungi o rimuovi filigrane o sfondi nelle pagine selezionate.
* Aggiungi o rimuovi intestazioni e piè di pagina nelle pagine selezionate.
* Rimuove la struttura e le funzionalità di navigazione di un Portfolio PDF Package o PDF. Il risultato è un singolo file PDF.
* Rinumera le etichette di pagina. Le etichette di pagina vengono in genere utilizzate per la numerazione delle pagine.
* Importa metadati da un altro documento di origine.
* Aggiungi o rimuovi file allegati, segnalibri, collegamenti, commenti e JavaScript.
* Impostare le caratteristiche della visualizzazione iniziale e ottimizzarle per la visualizzazione sul web.
* Impostare le autorizzazioni per PDF crittografato.
* Ruota le pagine o ruota e sposta il contenuto sulle pagine.
* Modificare le dimensioni delle pagine selezionate.
* Unisci i dati con un PDF basato su XFA.

È possibile utilizzare una semplice mappa di input per specificare le posizioni dei documenti di origine e dei documenti risultanti. Puoi anche utilizzare i seguenti tipi di URL dati esterni:

* File
* FTP
* HTTP/HTTPS

## Servizio di garanzia dei documenti {#doc-assurance-service}

Il servizio Controllo documenti consente di crittografare e decrittografare i documenti, estendere le funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi e aggiungere firme digitali ai documenti. Gli utenti possono interagire facilmente con PDF forms e documenti, mentre la tua organizzazione migliora la sicurezza, l&#39;archiviazione e la conformità.

Il servizio di garanzia documenti contiene tre servizi: firma, crittografia ed estensione del lettore.

### Servizio Firma {#signature-service}

Il servizio Signature consente di utilizzare firme digitali e documenti sul server AEM. Ad esempio, il servizio Firma viene generalmente utilizzato nelle situazioni seguenti:

* Il server AEM certifica un modulo prima che venga inviato a un utente per l’apertura utilizzando Acrobat o Adobe Reader.
* Il server AEM convalida una firma aggiunta a un modulo utilizzando Acrobat o Adobe Reader.
* Il server AEM firma un modulo per conto di un notaio pubblico.

Il servizio Signature accede ai certificati e alle credenziali archiviati nell&#39;archivio trusted.

### Servizio Encryption {#encryption-service}

Il servizio di crittografia consente di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. È possibile cifrare l’intero documento PDF (compresi il relativo contenuto, metadati e allegati), qualsiasi elemento diverso dai relativi metadati o solo gli allegati. Un utente autorizzato può decrittografare il documento per ottenere l&#39;accesso ai relativi contenuti. Se un documento PDF è crittografato con una password, è necessario specificare la password aperta prima di poter visualizzare il documento in Adobe Reader o Acrobat. Se un documento PDF è crittografato con un certificato, l’utente deve decrittografare il documento PDF con una chiave privata (certificato). La chiave privata utilizzata per decrittografare il documento PDF deve corrispondere alla chiave pubblica utilizzata per crittografarlo.

### Servizio di estensione del Reader {#reader-extension-service}

Il servizio Estensioni di Reader consente alla tua organizzazione di condividere facilmente documenti PDF interattivi estendendo la funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi. Il servizio Estensioni di Reader funziona con Adobe Reader 7.0 o versione successiva. Il servizio aggiunge diritti di utilizzo a un documento PDF. Questa azione attiva le funzioni solitamente non disponibili quando un documento PDF viene aperto con Adobe Reader, ad esempio l’aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento. Gli utenti di terze parti non richiedono software o plug-in aggiuntivi per lavorare con documenti abilitati per i diritti.

Quando ai documenti PDF vengono aggiunti i diritti di utilizzo appropriati, i destinatari possono eseguire le seguenti attività direttamente da Adobe Reader:

* Compilare documenti e moduli PDF online o offline, consentendo ai destinatari di salvare copie localmente per i propri record e mantenendo intatte le informazioni aggiunte
* Salvare i documenti PDF in un disco rigido locale per conservare il documento originale ed eventuali commenti, dati o allegati aggiuntivi
* Allegare file e clip multimediali a documenti PDF
* Firma, certificazione e autenticazione dei documenti PDF applicando firme digitali utilizzando tecnologie PKI (Public Key Infrastructure) standard del settore
* Invio elettronico di documenti PDF completati o annotati
* Utilizzare i documenti e i moduli di PDF come front-end di sviluppo intuitivo per database interni e servizi web
* Condividere documenti PDF con altri utenti in modo che i revisori possano aggiungere commenti utilizzando strumenti di marcatura intuitivi. Questi strumenti includono note adesive elettroniche, timbri, evidenziazioni e barrato di testo. Le stesse funzioni sono disponibili in Acrobat.
* È supportata la decodifica dei moduli con codice a barre.

Queste funzionalità speciali vengono attivate automaticamente quando un documento PDF abilitato per i diritti viene aperto in Adobe Reader. Quando l’utente ha finito di lavorare con un documento abilitato per i diritti, tali funzioni vengono nuovamente disattivate in Adobe Reader. Rimangono disabilitate finché l’utente non riceve un altro documento PDF con diritti abilitati.

Il servizio DocAssurance non è disponibile per l&#39;utilizzo. Per configurare il servizio DocAssurance, vedere [Installazione e configurazione di Document Services](../../forms/using/install-configure-document-services.md).

## Invia a servizio stampante {#send-to-printer-service}

Il servizio Invia a stampante fornisce l&#39;API per l&#39;invio di documenti a una stampante specifica per la stampa.
