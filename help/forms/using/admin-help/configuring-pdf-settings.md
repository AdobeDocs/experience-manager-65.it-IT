---
title: Configurazione delle impostazioni di Adobe PDF
seo-title: Configuring Adobe PDF settings
description: Scopri come configurare le impostazioni di Adobe PDF.
seo-description: Learn how to configure Adobe PDF settings.
uuid: 980c9d6a-f75e-4e7d-b050-d2d07a10ef33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab018b6d-0233-4439-bb75-58c5421d769a
feature: PDF Generator
exl-id: 1bcb8429-c06e-4bd3-b422-4c512084dd09
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '7265'
ht-degree: 0%

---

# Configurazione delle impostazioni di Adobe PDF{#configuring-adobe-pdf-settings}

La pagina Impostazioni di Adobe PDF mostra le impostazioni di conversione che puoi specificare per le sorgenti da utilizzare. È possibile utilizzare una qualsiasi delle impostazioni PDF predefinite o crearne una personalizzata. Le impostazioni di PDF determinano con precisione la modalità di conversione dei file e la struttura e le caratteristiche di PDF risultanti. Le impostazioni di Adobe PDF erano precedentemente note come parametri Distiller® o opzioni di lavoro.

Nella pagina Impostazioni di Adobe PDF puoi effettuare le seguenti operazioni:

* Visualizzare le impostazioni predefinite di PDF. (Vedi [Informazioni sulle impostazioni PDF predefinite](configuring-pdf-settings.md#about-the-predefined-pdf-settings).)
* Creare un’impostazione di PDF o modificarne una creata in precedenza. (Vedi [Aggiungere o modificare le impostazioni di PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).)
* Specificare le impostazioni PDF predefinite. (Vedi [Modificare le impostazioni predefinite](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings))
* Carica un file delle impostazioni di PDF sul server. (Vedi [Carica le impostazioni di PDF](configuring-pdf-settings.md#upload-pdf-settings).)
* Elimina le impostazioni personalizzate di PDF. (Vedi [Eliminare le impostazioni di PDF](configuring-pdf-settings.md#delete-pdf-settings).)
* Carica e scarica file prolog ed epilog. (Vedi [Caricamento e download di file prolog ed epilog](configuring-pdf-settings.md#uploading-and-downloading-prologue-and-epilogue-files).)

Le impostazioni Adobe PDF sono applicabili solo alle conversioni basate su PDFMaker. Queste includono le seguenti conversioni:

* Documento Word Microsoft (DOC, DOCX, RTF, TXT)
* Documento Microsoft Excel (XLS, XLSX)
* Documento Microsoft PowerPoint (PPT, PPTX)
* Documento di progetto Microsoft (MPP)
* Documento di Microsoft Visio (VSD)

>[!NOTE]
>
>Quando si utilizza OpenOffice per convertire i formati di cui sopra, le impostazioni Adobe PDF non vengono applicate.

## Informazioni sulle impostazioni PDF predefinite {#about-the-predefined-pdf-settings}

PDF Generator fornisce diverse impostazioni PDF predefinite per l’utilizzo. Non è possibile modificare queste impostazioni predefinite; tuttavia, puoi creare un’impostazione basata su una esistente modificando l’impostazione e salvandola con un nuovo nome.

**Stampa di alta qualità:** Crea file PDF per un output di alta qualità. Questa impostazione:

* esegue il downsample delle immagini a colori e in scala di grigi a 300 dpi
* esegue il downsample di immagini monocromatiche a 1200 dpi
* stampa a una risoluzione immagine più elevata
* utilizza altre impostazioni per mantenere la quantità massima di informazioni sul documento originale.

Questi file PDF possono essere aperti in Adobe Acrobat 5 e Adobe Acrobat Reader® 5 o versione successiva.

**Pagine di grandi dimensioni:** Crea documenti PDF adatti per la visualizzazione e la stampa affidabili di disegni tecnici di dimensioni superiori a 200 x 200 pollici. I documenti PDF creati possono essere aperti in Adobe Acrobat Professional e Acrobat Standard, versione 7 o successiva e Adobe Reader 7 o versioni successive.

**PDF/A-1B 2005 CMYK / PDF/A-1B 2005 RGB:** Controlla i lavori in arrivo per la conformità allo standard ISO per la conservazione a lungo termine (archiviazione) dei documenti elettronici e crea file PDF/A solo se conformi. Questi file vengono utilizzati principalmente per l&#39;archiviazione. I file conformi possono contenere solo testo, immagini raster e oggetti vettoriali; non possono contenere cifratura e script. Inoltre, tutti i font devono essere incorporati in modo che i documenti possano essere aperti e visualizzati come creati. PDF/A-1b utilizza PDF 1.4 e converte tutti i colori in CMYK o RGB, a seconda dello standard scelto. I file PDF creati con questo file di impostazioni possono essere aperti in Acrobat 5 e Acrobat Reader 5 e versioni successive. Per ulteriori informazioni su PDF/A, consulta Adobi e standard di settore.

**PDF/X-1a 2001:** Controlla i processi in arrivo per la conformità di PDF/X-1a e crea file PDF solo se conformi. PDF/X-1a è uno standard ISO per lo scambio di contenuti grafici. PDF/X-1a richiede l’incorporazione di tutti i font, la specificazione delle caselle PDF appropriate e l’aspetto del colore come CMYK o colori campione. I file PDF che soddisfano i requisiti PDF/X-1a sono destinati a una specifica condizione di output, ad esempio la stampa offset web in base alle specifiche Pubblicazioni offset web. Per ulteriori informazioni su PDF/X, consulta Adobi e standard di settore.

**PDF/X-3 2002:** Controlla i processi in arrivo per la conformità PDF/X-3 e crea file PDF solo se conformi. Come PDF/X-1a, PDF/X-3 è uno standard ISO per lo scambio di contenuti grafici. La differenza principale è che PDF/X-3 supporta il colore indipendente dal dispositivo.

**Qualità della stampa:** Crea file PDF per la produzione di stampe di alta qualità (ad esempio, su un dispositivo di acquisizione immagini o su un dispositivo di stampa). In questo caso, la dimensione del file non viene presa in considerazione. L&#39;obiettivo è quello di mantenere tutte le informazioni in un file PDF che una stampante commerciale o un fornitore di servizi di prestampa deve stampare correttamente il documento. Questo insieme di opzioni:

* esegue il downsample delle immagini a colori e in scala di grigi a 300 dpi
* esegue il downsample di immagini monocromatiche a 1200 dpi
* incorpora sottoinsiemi di tutti i font utilizzati nel documento
* stampa a una risoluzione più elevata dell&#39;immagine,
* non ruota automaticamente le pagine in base all&#39;orientamento dei commenti delle convenzioni di strutturazione del testo o del documento (DSC)
* utilizza altre impostazioni per mantenere la quantità massima di informazioni sul documento originale.

I processi di stampa non riescono se contengono font che non possono essere incorporati. Questi file PDF possono essere aperti in Acrobat 5 e Acrobat Reader 5 e versioni successive.

>[!NOTE]
>
>Prima di creare un file PDF da inviare a una stampante commerciale o a un provider di servizi di prestampa, determinare la risoluzione di output e altre impostazioni o richiedere un file .joboptions con le impostazioni consigliate. Potrebbe essere necessario personalizzare le impostazioni di Adobe PDF per un particolare provider e quindi fornire un file .joboptions personale.

**Dimensioni file più piccole:** Crea file PDF per la visualizzazione sul Web o su una Intranet o per la distribuzione tramite un sistema e-mail per la visualizzazione sullo schermo. Questa serie di opzioni utilizza la compressione, il downsampling e una risoluzione dell&#39;immagine relativamente bassa. Converte tutti i colori in sRGB e non incorpora i font se necessario. Ottimizza anche i file per il servizio byte. Questi file PDF possono essere aperti in Acrobat 5 e Acrobat Reader 5.0 e versioni successive.

**Standard:** Crea file PDF da stampare su stampanti desktop o fotocopiatrici digitali, pubblicare su CD o inviare a un client come prova di pubblicazione. Questo insieme di opzioni utilizza la compressione e il downsampling per ridurre le dimensioni del file. Incorpora anche sottoinsiemi di tutti i font utilizzati nel file, converte tutti i colori in sRGB e stampa a una risoluzione media per creare una rappresentazione ragionevolmente accurata del documento originale. I sottoinsiemi di font Microsoft Windows non sono incorporati per impostazione predefinita. Questi file PDF possono essere aperti in Acrobat 5 e Acrobat Reader 5.0 e versioni successive.

## Aggiungere o modificare le impostazioni di PDF {#add-or-edit-pdf-settings}

Le impostazioni di PDF determinano con precisione la modalità di conversione dei file e la struttura e le caratteristiche di PDF risultanti. Definire una nuova impostazione di PDF o modificarne una creata in precedenza. Non è possibile modificare le impostazioni predefinite, ma è possibile creare un&#39;impostazione basata su una esistente modificando l&#39;impostazione e salvandola con un nuovo nome.

1. Nella console di amministrazione, fai clic su Servizi > Generatore PDF > Impostazioni Adobe PDF.
1. Fare clic su Nuovo oppure sul nome di un&#39;impostazione esistente.
1. Nella pagina Nuova/Modifica impostazione Adobe PDF , completa le informazioni richieste nelle sezioni seguenti:

[Opzioni generali](configuring-pdf-settings.md#general-options)

[Opzioni immagini](configuring-pdf-settings.md#images-options)

[Opzioni dei font](configuring-pdf-settings.md#fonts-options)

[Opzioni colore](configuring-pdf-settings.md#color-options)

[Opzioni avanzate](configuring-pdf-settings.md#advanced-options)

[Indicazioni sugli standard e opzioni di conformità](configuring-pdf-settings.md#standards-reporting-and-compliance-options)

[Opzioni della vista iniziale](configuring-pdf-settings.md#initial-view-options)

   Per passare a un’altra sezione, fai clic sul relativo collegamento nella pagina Web o utilizza i pulsanti Successivo e Precedente .

1. Dopo aver completato le informazioni in tutte le sezioni, fai clic su Salva o su Salva con nome e specifica un nome per l’impostazione.

## Carica le impostazioni di PDF {#upload-pdf-settings}

È possibile disporre delle impostazioni PDF disponibili sul server PDF Generator caricandole da un computer locale o da un percorso di rete.

1. Nella console di amministrazione, fai clic su Servizi > Generatore di PDF > Impostazioni Adobe PDF e fai clic su Carica.
1. Nella pagina Carica impostazione Adobe PDF fare clic su Sfoglia, individuare il file delle impostazioni di PDF e fare clic su Apri.
1. Fare clic su OK, quindi di nuovo su OK.

## Eliminare le impostazioni di PDF {#delete-pdf-settings}

Se non sono più necessarie, è possibile eliminare definitivamente le impostazioni di PDF.

1. Nella console di amministrazione, fai clic su Servizi > Generatore PDF > Impostazioni Adobe PDF.
1. Seleziona la casella di controllo accanto all’impostazione da eliminare. È possibile selezionare più impostazioni.
1. Fare clic su Elimina e, nella pagina Elimina conferma, fare di nuovo clic su Elimina.

## Opzioni generali {#general-options}

Utilizza le opzioni generali per specificare la versione di Acrobat da utilizzare per la compatibilità dei file e altre opzioni di file e dispositivi. Per istruzioni su come accedere alle opzioni Generali, consulta [Aggiungere o modificare le impostazioni di PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Opzioni file {#file-options}

**Compatibilità:** Livello di compatibilità del file PDF. Per i documenti che saranno ampiamente distribuiti, è consigliabile selezionare Acrobat 4 (PDF 1.3) o Acrobat 5 (PDF 1.4) per garantire che tutti gli utenti possano visualizzare e stampare il documento. Se si creano file utilizzando la compatibilità Acrobat 5 o versioni successive, è possibile che questi non siano compatibili con le versioni precedenti di Acrobat. Le sottosezioni seguenti mostrano alcune delle differenze tra i file PDF creati utilizzando diversi livelli di compatibilità di Acrobat.

<table>
 <tbody>
  <tr>
   <th><p>Acrobat 4 (PDF 1.3)</p> </th>
   <th><p>Acrobat 5 (PDF 1.4)</p> </th>
   <th><p>Acrobat 6 (PDF 1.5)</p> </th>
   <th><p>Acrobat 7 (PDF 1.6) e Acrobat 8 (PDF 1.7)</p> </th>
  </tr>
  <tr>
   <td><p>Può essere aperto con Acrobat 3.0 e Acrobat Reader 3.0 e versioni successive.</p> </td>
   <td><p>Può essere aperto con Acrobat 3.0 e Acrobat Reader 3.0 e versioni successive. Le funzioni specifiche delle versioni successive potrebbero essere perse o non essere visualizzate.</p> </td>
   <td><p>La maggior parte può essere aperta con Acrobat 4 e Acrobat Reader 4.0 e versioni successive. Le funzioni specifiche delle versioni successive potrebbero essere perse o non essere visualizzate.</p> </td>
   <td><p>La maggior parte può essere aperta con Acrobat 4 e Acrobat Reader 4.0 e versioni successive. Le funzioni specifiche delle versioni successive potrebbero essere perse o non essere visualizzate.</p> </td>
  </tr>
  <tr>
   <td><p>Non può contenere immagini che utilizzano effetti di trasparenza in tempo reale. Qualsiasi trasparenza deve essere appiattita prima di convertirla in PDF 1.3.</p> </td>
   <td><p>Sostiene l'uso della trasparenza in tempo reale nelle opere d'arte. La funzione Acrobat Distiller appiattisce la trasparenza.</p> </td>
   <td><p>Sostiene l'uso della trasparenza in tempo reale nelle opere d'arte. La funzione Acrobat Distiller appiattisce la trasparenza.</p> </td>
   <td><p>Sostiene l'uso della trasparenza in tempo reale nelle opere d'arte. La funzione Acrobat Distiller appiattisce la trasparenza.</p> </td>
  </tr>
  <tr>
   <td><p>I livelli non sono supportati.</p> </td>
   <td><p>I livelli non sono supportati.</p> </td>
   <td><p>Mantiene i livelli durante la creazione di file PDF da applicazioni che supportano la generazione di documenti PDF a livelli, ad esempio Adobe Illustrator® CS o Adobe InDesign® CS e versioni successive.</p> </td>
   <td><p>Mantiene i livelli durante la creazione di file PDF da applicazioni che supportano la generazione di documenti PDF a livelli, come Illustrator CS o InDesign CS e versioni successive.</p> </td>
  </tr>
  <tr>
   <td><p>È supportato lo spazio colore DeviceN con 8 coloranti.</p> </td>
   <td><p>È supportato lo spazio colore DeviceN con 8 coloranti.</p> </td>
   <td><p>È supportato lo spazio colore DeviceN con fino a 31 coloranti.</p> </td>
   <td><p>È supportato lo spazio colore DeviceN con fino a 31 coloranti.</p> </td>
  </tr>
  <tr>
   <td><p>I font multibyte possono essere incorporati. (Distiller converte i font durante l’incorporazione).</p> </td>
   <td><p>I font multibyte possono essere incorporati.</p> </td>
   <td><p>I font multibyte possono essere incorporati.</p> </td>
   <td><p>I font multibyte possono essere incorporati.</p> </td>
  </tr>
  <tr>
   <td><p>È supportata la sicurezza RC4 a 40 bit.</p> </td>
   <td><p>È supportata la sicurezza RC4 a 128 bit.</p> </td>
   <td><p>È supportata la sicurezza RC4 a 128 bit.</p> </td>
   <td><p>Protezione RC4 a 128 bit e AES a 128 bit (Advanced Encryption Standard) supportata.</p> </td>
  </tr>
 </tbody>
</table>

**Compressione a livello di oggetto:** Consolida piccoli oggetti (ciascuno dei quali non è comprimibile) in flussi che possono quindi essere compressi in modo efficiente.

**Disattivato:** Non comprime informazioni strutturali nel documento PDF. Seleziona questa opzione se desideri che gli utenti visualizzino, navigino e interagiscano con segnalibri e altre informazioni strutturali utilizzando Acrobat 5 e versioni successive.

**Solo tag:** Comprime le informazioni strutturali nel documento PDF. L’utilizzo di questa opzione consente di aprire e stampare un file PDF utilizzando Acrobat 5. Gli utenti non possono visualizzare informazioni su accessibilità, struttura o PDF con tag in Acrobat 5 o Acrobat Reader 5.0, ma possono visualizzarle in Acrobat 6 e Adobe Reader 6.0.

**Ruota automaticamente le pagine:** Imposta la rotazione automatica delle pagine in base all’orientamento del testo o dei commenti DSC. Ad esempio, per alcune pagine (ad esempio le pagine che contengono tabelle) potrebbe essere necessario che l’utente le ruoti lateralmente per leggerle. Selezionare Singolarmente per ruotare ogni pagina in base alla direzione del testo nella pagina. Selezionare Collettivamente per file per ruotare tutte le pagine del documento in base all’orientamento della maggior parte del testo.

>[!NOTE]
>
>Se nelle impostazioni avanzate sono selezionati Commenti DSC processo e se sono inclusi i commenti di orientamento %%Viewing, questi commenti hanno la precedenza nel determinare l&#39;orientamento della pagina.

**Binding:** Specifica se visualizzare un file PDF con binding a sinistra o a destra. Questa impostazione ha effetto sulla visualizzazione delle pagine nel layout Facing Page - Continuous e sulla visualizzazione delle miniature affiancate.

**Risoluzione:** Imposta l&#39;emulazione per la risoluzione di una stampante per i file di input che regolano il loro comportamento in base alla risoluzione della stampante su cui stanno stampando. Per la maggior parte dei file di input, un’impostazione di risoluzione più elevata genera file PDF di qualità maggiore ma più grandi e un’impostazione più bassa genera file PDF di qualità inferiore. Nella maggior parte dei casi, la risoluzione determina il numero di passaggi in una sfumatura o miscela. È possibile immettere un valore compreso tra 72 e 4000. Mantenere questa impostazione come predefinita a meno che non si intenda stampare il file PDF su una stampante specifica e si desideri emulare la risoluzione definita nel file di input originale.

>[!NOTE]
>
>L&#39;aumento dell&#39;impostazione della risoluzione aumenta le dimensioni del file e può leggermente aumentare il tempo necessario per elaborare alcuni file.

**Tutte le pagine o le pagine da:** Specifica le pagine da convertire. Lasciare vuota la casella A per creare un intervallo dal numero di pagina immesso nella casella Da alla fine del file.

**Ottimizza Per Visualizzazione Web Rapida:** Ristruttura il file per il download della pagina alla volta (byte serving) dai server web. Questa opzione comprime il testo e la grafica a linee, indipendentemente dalle impostazioni di compressione selezionate nella scheda Immagini. La compressione consente un accesso e una visualizzazione più veloci durante il download del file dal web o da una rete. Per impostazione predefinita, questa opzione non è abilitata.

### Dimensioni pagina predefinite {#default-page-size}

Le opzioni Dimensione pagina predefinita specificano la dimensione della pagina da utilizzare quando non è specificata nel file originale. In genere, i file Adobe PostScript includono queste informazioni, ad eccezione dei file Encapsulated PostScript (EPS), che danno una dimensione del riquadro di delimitazione ma non una dimensione della pagina. La dimensione massima consentita della pagina è di 15.000.000 pollici (31.800.000 cm) in entrambe le direzioni. Queste opzioni configurano le dimensioni predefinite della pagina:

**Larghezza:** Larghezza della pagina

**Altezza:** Altezza della pagina

**Unità:** Unità da utilizzare per le impostazioni di larghezza e altezza

## Opzioni immagini {#images-options}

Le opzioni Immagini specificano la compressione e il ricampionamento delle immagini. È possibile sperimentare queste opzioni per trovare un equilibrio appropriato tra la dimensione del file e la qualità dell&#39;immagine. Per istruzioni su come accedere alle impostazioni delle immagini, consulta [Aggiungere o modificare le impostazioni di PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Queste opzioni consentono di configurare immagini a colori, in scala di grigi e monocromatiche:

**Downsample:** Imposta un valore per ogni tipo di immagine. Per eseguire il downsample di immagini a colori, in scala di grigi o monocromatiche, PDF Generator combina i pixel in un&#39;area campione per ingrandire un pixel. Fornire la risoluzione del dispositivo di output in punti per pollice (dpi) e immettere una risoluzione in dpi nella casella Per immagini sopra. Per le immagini con una risoluzione superiore a questa soglia, PDF Generator combina i pixel, in base alle esigenze, per ridurre la risoluzione dell&#39;immagine (pixel per pollice) all&#39;impostazione dpi specificata. Per disattivare il sottocampionamento, selezionare Disattivato. Di seguito sono riportate le opzioni disponibili:

**Downsampling medio a:** Media i pixel di un&#39;area campione e sostituisce l&#39;intera area con il colore medio dei pixel alla risoluzione specificata.

**Campionamento Bicubico A:** Utilizza una media ponderata per determinare il colore dei pixel e in genere produce risultati migliori rispetto al metodo di calcolo della media semplice del downsampling. Bicubica è il metodo più lento ma più preciso e si traduce in gradazioni tonali più uniformi.

**Sottocampionamento A:** Seleziona un pixel al centro dell&#39;area campione e sostituisce l&#39;intera area con tale pixel alla risoluzione specificata. Il sottocampionamento riduce in modo significativo il tempo di conversione rispetto al sottocampionamento, ma genera immagini meno uniformi e continue.

L&#39;impostazione della risoluzione per colore e scala di grigi deve essere da 1,5 a 2 volte la regola dello schermo della linea in cui il file verrà stampato. (A condizione che non si vada al di sotto di questa impostazione di risoluzione consigliata, le immagini che non contengono linee rette o motivi geometrici o ripetuti non sono influenzate da una risoluzione inferiore.) La risoluzione per le immagini monocromatiche dovrebbe essere la stessa del dispositivo di output. Tuttavia, il salvataggio di un&#39;immagine monocromatica a una risoluzione superiore a 1500 dpi aumenta le dimensioni del file senza migliorare sensibilmente la qualità dell&#39;immagine.

Inoltre, considera se gli utenti devono ingrandire una pagina. Ad esempio, se si crea un documento PDF di una mappa, è consigliabile utilizzare una risoluzione immagine più elevata in modo che gli utenti possano ingrandire la mappa.

>[!NOTE]
>
>Il ricampionamento delle immagini monocromatiche può produrre risultati di visualizzazione imprevisti, ad esempio nessuna visualizzazione delle immagini. Se si verifica questo problema, disattivare il ricampionamento e convertire di nuovo il file. Questo problema si verifica con maggiore probabilità con il sottocampionamento e con minore probabilità con il sottocampionamento bicubico.

Questa tabella mostra i tipi di stampanti e la loro risoluzione misurata in dpi, la loro regola dello schermo predefinita misurata in linee per pollice (lpi) e una risoluzione di ricampionamento per le immagini misurate in pixel per pollice (ppi). Ad esempio, per stampare su una stampante laser a 600 dpi, immettere 170 per la risoluzione in cui campionare le immagini.

<table>
 <tbody>
  <tr>
   <th><p>Risoluzione della stampante</p> </th>
   <th><p>Schermata a linee predefinita</p> </th>
   <th><p>Risoluzione dell'immagine</p> </th>
  </tr>
  <tr>
   <td><p>300 dpi (stampante laser)</p> </td>
   <td><p>60 lpi</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi (stampante laser)</p> </td>
   <td><p>85 lpi</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200 dpi (fotounità)</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 dpi (fotounità)</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

**Compressione:** Imposta un valore da applicare alle immagini a colori, in scala di grigi e monocromatiche. Per le immagini a colori e in scala di grigi, imposta anche la qualità dell&#39;immagine:

* Per le immagini a colori o in scala di grigi, selezionare ZIP per applicare una compressione che funzioni bene sulle immagini che hanno grandi aree di singoli colori o pattern ripetuti. Esempi sono le immagini a schermo, le immagini semplici create con programmi di pittura e le immagini monocromatiche che contengono pattern ripetuti. Selezionare JPEG, qualità minima fino al massimo, per applicare una compressione adatta per immagini in scala di grigi o a colori, ad esempio fotografie a tonalità continua che contengono più dettagli di quelli che possono essere riprodotte sullo schermo o nella stampa. Selezionare Automatico (JPEG) per determinare automaticamente la migliore qualità per le immagini a colori e in scala di grigi.
* Per le immagini monocromatiche, selezionare CCITT Group 4, CCITT Group 3, ZIP, JPEG200, Automatic (JPEG2000) o Esegui la compressione Length.

Assicurati che le immagini monocromatiche siano scansionate come monocromatiche e non come scala di grigi. Per impostazione predefinita, il testo digitalizzato viene talvolta salvato come immagini in scala di grigi. Il testo in scala di grigi compresso con il metodo di compressione JPEG non è chiaro e potrebbe essere illeggibile.

**Qualità immagine:** Configura la qualità dell&#39;immagine per le immagini a colori e in scala di grigi. Le opzioni sono minime, basse, medie, alte e massime.

**Anti-alias A Grigio:** Smussano bordi frastagliati nelle immagini monocromatiche. Selezionare 2 bit, 4 bit o 8 bit per specificare 4, 16 o 256 livelli di grigio. (L&#39;anti-aliasing può sfocare linee sottili o di tipo piccolo.)

>[!NOTE]
>
>La compressione del testo e della grafica a linee è sempre attiva.

**Criterio immagine:** Imposta un criterio per le immagini a colori, in scala di grigi e monocromatiche. Se la risoluzione dell&#39;immagine è inferiore alla risoluzione specificata, è comunque possibile selezionare di continuare (Ignora), inviare un messaggio di avviso o annullare il processo.

## Opzioni dei font {#fonts-options}

Le opzioni Font specificano i font da incorporare in un file PDF e se incorporare un sottoinsieme di caratteri utilizzati nel file PDF. Per istruzioni su come accedere alle opzioni Font, consulta [Aggiungere o modificare le impostazioni di PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

>[!NOTE]
>
>Quando si combinano file PDF con lo stesso sottoinsieme di font, PDF Generator tenta di combinare i sottoinsiemi di font.

**Incorpora tutti i font:** Incorpora tutti i font utilizzati nel file. L&#39;incorporazione dei font è necessaria per la conformità PDF/X.

**Sottoinsieme Font Incorporati Quando La Percentuale Di Caratteri Utilizzati È Inferiore A:** Se selezioni questa opzione, specifica una percentuale di soglia per incorporare solo un sottoinsieme dei font. Ad esempio, se la soglia è il 35% e vengono utilizzati meno del 35% dei caratteri, PDF Generator incorpora solo tali caratteri. Vengono incorporati solo i font con i bit di autorizzazione appropriati.

**Quando L’Incorporazione Non Riesce:** Specifica la risposta di PDF Generator se non è in grado di trovare un font da incorporare durante l’elaborazione di un file. È possibile fare in modo che PDF Generator ignori la richiesta e sostituisca il font, avvisi e sostituisca il font oppure annulli l’elaborazione del lavoro corrente.

**Origine font:** La posizione dei font utilizzati da PDF Generator.

### Specificare i font da incorporare {#specify-which-fonts-to-embed}

1. Nella console di amministrazione, fai clic su Servizi > Generatore PDF > Impostazioni Adobe PDF.
1. Fare clic su Nuovo o sul nome di un&#39;impostazione.
1. Fare clic su Font e deselezionare Incorpora tutti i font.
1. Dall&#39;elenco Origine font, selezionare un&#39;origine font e fare clic su Vai per aggiornare l&#39;elenco dei font nella casella a sinistra.
1. Fare clic su un font nella casella a sinistra. Quindi fai clic su Aggiungi accanto alla casella appropriata per spostarla nell’elenco Incorpora sempre o Non incorporare mai . Ripetere la procedura per ogni font. Premere Ctrl per selezionare più font da spostare.
1. Per rimuovere un font dall’elenco Incorpora sempre o Non incorporare, selezionalo e fai clic su Rimuovi accanto alla casella appropriata. Questa azione non rimuove il font dal sistema; rimuove il riferimento nell&#39;elenco.
1. Se il font che si desidera specificare non viene visualizzato, digitare il nome nella casella Aggiungi carattere e quindi fare clic su Incorpora sempre o Non incorporare mai. I nomi dei font non possono contenere caratteri alfanumerici.

>[!NOTE]
>
>Un font TrueType può contenere un&#39;impostazione aggiunta dal designer del font che impedisce l&#39;incorporazione del font nei file di PDF.

>[!NOTE]
>
>I font vengono selezionati dalla cache dei font di sistema di Windows ed è necessario un riavvio del sistema per aggiornare la cache. Dopo aver specificato la directory dei font per il cliente, assicurarsi di riavviare il sistema in cui sono installati AEM moduli.

## Opzioni colore {#color-options}

Le opzioni Colore impostano tutte le informazioni sulla gestione del colore per PDF Generator. Per istruzioni su come accedere alle opzioni di colore, consulta [Aggiungere o modificare le impostazioni di PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Impostazioni di Adobe Color {#adobe-color-settings}

**File impostazioni:** Questo elenco contiene un elenco delle impostazioni colore utilizzate anche nelle principali applicazioni grafiche, come Adobe Photoshop e Adobe Illustrator. L&#39;impostazione del colore selezionata determina le altre impostazioni del colore Adobe in questa pagina. Ad esempio, se selezioni un’impostazione diversa da Nessuno, tutte le opzioni diverse da quelle per Dati dipendenti dal dispositivo sono predefinite e disattivate. È possibile modificare le impostazioni Criteri di gestione del colore e Spazi di lavoro solo se si seleziona Nessuno per File impostazioni.

### Criteri di gestione del colore {#color-management-policies}

Se si seleziona Nessuno per il file impostazioni, l&#39;area Criteri di gestione del colore specifica il modo in cui PDF Generator converte i colori non gestiti in un file PostScript.

**Lascia colore non modificato:** Lascia invariati i colori dipendenti dalla periferica e conserva i colori indipendenti dalla periferica come equivalente più vicino possibile in PDF. Questa opzione è utile per i laboratori di stampa che hanno calibrato tutti i loro dispositivi, utilizzato quelle informazioni per specificare il colore nel file e l&#39;output solo per quei dispositivi.

**Assegna tag a tutto per la gestione del colore:** Incorpora un profilo International Color Consortium durante la distillazione dei file e calibra il colore nelle immagini, il che rende i colori nei file PDF risultanti indipendenti dalla periferica se hai selezionato Acrobat 4 (PDF 1.3) o una compatibilità successiva. Tuttavia, gli spazi colore dipendenti dalla periferica nei file (RGB, Scala di grigio e CMYK) vengono convertiti in spazi colore indipendenti dalla periferica (CalRGB, CalGray e LAB).

**Assegnare tag solo alle immagini per la gestione del colore:** Durante la distribuzione dei file, incorpora i profili ICC solo nelle immagini, non nel testo o nella grafica, se hai selezionato la compatibilità Acrobat 4 (PDF 1.3). Questa opzione impedisce al testo nero di subire uno spostamento del colore. Tuttavia, gli spazi colore dipendenti dalla periferica nelle immagini (RGB, Scala di grigio e CMYK) vengono convertiti in spazi colore indipendenti dalla periferica (CalRGB, CalGray e LAB). Il testo e gli elementi grafici non vengono convertiti.

**Converti tutti i colori in sRGB o converti tutti i colori in CMYK:** Calibra il colore nel file, rendendo il colore indipendente dalla periferica, simile a Tag Tutto per la gestione del colore. Se hai selezionato Compatibilità Acrobat 4 (PDF 1.3) o versioni successive e hai convertito in sRGB, le immagini CMYK e RGB vengono convertite in sRGB.

Indipendentemente dall’opzione di compatibilità selezionata, le immagini in scala di grigi vengono lasciate invariate. Questo di solito riduce le dimensioni e aumenta la velocità di visualizzazione dei file PDF, perché sono necessarie meno informazioni per descrivere le immagini RGB che per descrivere le immagini CMYK. Poiché RGB è lo spazio colore nativo utilizzato sui monitor, non è necessaria alcuna conversione del colore durante la visualizzazione, il che contribuisce a una rapida visualizzazione online. Questa opzione è consigliata se il file PDF è per l’uso online o con stampanti a bassa risoluzione.

**Intento di rendering del documento:** Metodo per mappare i colori tra gli spazi colore. Il risultato di un particolare metodo dipende dai profili degli spazi colore. Ad esempio, alcuni profili producono risultati identici con metodi diversi. Le opzioni disponibili sono:

>[!NOTE]
>
>In tutti i casi, gli intenti possono essere ignorati o ignorati dalle operazioni di gestione del colore che si verificano dopo la creazione del file PDF.

**Mantieni:** Indica che l&#39;intento è specificato nel dispositivo di output anziché nel file PDF. In molti dispositivi di output, l&#39;intento predefinito è Colorimetrico relativo.

**Percettivo:** Mantiene i valori di colore relativi tra i pixel originali mentre sono mappati sulla gamma di destinazione. Questo metodo conserva la relazione visiva tra i colori, anche se i valori dei colori stessi possono cambiare.

**Saturazione:** Mantiene i valori di saturazione relativi dei pixel originali. Questo metodo è adatto per la grafica aziendale, in cui la relazione esatta tra i colori non è tanto importante quanto avere colori saturi brillanti.

**Colorimetrico relativo:** Consente di rimappare il punto bianco dello spazio sorgente al punto bianco dello spazio di destinazione.

**Colorimetrico assoluto:** Disattiva la corrispondenza dei punti bianchi e neri durante la conversione dei colori. Questo metodo è consigliato solo se è necessario conservare i colori della firma, ad esempio quelli utilizzati nei marchi o nei loghi.

### Spazi di lavoro {#working-spaces}

Per tutti i valori nell’elenco Criteri di gestione del colore, diversi da Lascia colore non modificato, selezionare dagli elenchi nell’area Area di lavoro per specificare quali profili ICC vengono utilizzati per definire e calibrare gli spazi di colore in scala di grigi, RGB e CMYK nei file PDF distillati. Le opzioni disponibili sono:

**Grigio:** Definisce lo spazio colore di tutte le immagini in scala di grigi nei file. Questa opzione è disponibile solo se si è scelto Tag tutto per la gestione del colore o Tag solo immagini per la gestione del colore. Il profilo ICC predefinito per le immagini in grigio è Gamma 2.2. È inoltre possibile selezionare Nessuno per impedire la conversione delle immagini in scala di grigi.

**RGB:** Definisce lo spazio colore di tutte le immagini RGB nei file. Il valore predefinito, sRGB IEC61966-2.1, è generalmente una buona scelta perché sta diventando uno standard di settore e molti dispositivi di uscita lo riconoscono. È inoltre possibile selezionare Nessuno per impedire la conversione delle immagini RGB.

**CMYK:** Definisce lo spazio colore di tutte le immagini CMYK nei file. Il valore predefinito è US Web Coated (SWOP) v2. È inoltre possibile selezionare Nessuno per impedire la conversione delle immagini CMYK.

>[!NOTE]
>
>La selezione di Nessuno per tutti e tre gli spazi di lavoro ha lo stesso effetto della selezione di Lascia colore non modificato.

**Mantieni valori CMYK per gli spazi colore CMYK calibrati:** Quando è selezionata questa opzione, i valori CMYK indipendenti dalla periferica vengono trattati come valori dipendenti dalla periferica (DeviceCMYK), gli spazi colore indipendenti dalla periferica vengono scartati e i file PDF/X-1a utilizzano il valore Converti tutti i colori in CMYK. Se deselezionati, gli spazi colore indipendenti dalla periferica vengono convertiti in CMYK se il criterio di gestione del colore è impostato su Converti tutti i colori in CMYK.

### Dati dipendenti dal dispositivo {#device-dependent-data}

Queste opzioni si applicano se si lavora con documenti creati con applicazioni grafiche e di documentazione di fascia alta, come Adobe Illustrator e Adobe InDesign. Per ulteriori informazioni, consulta la documentazione allegata all’applicazione.

Le funzioni di trasferimento sono utilizzate per l&#39;effetto artistico e per regolare le specifiche di un dispositivo di output specifico. Ad esempio, un file destinato all&#39;output su una particolare fotounità può contenere funzioni di trasferimento che compensano il guadagno del punto intrinseco alla stampante.

**Mantieni Sotto La Rimozione Del Colore E La Generazione Del Nero:** Mantiene queste impostazioni se presenti nel file PostScript. La generazione del nero calcola la quantità di nero da utilizzare quando si tenta di riprodurre un particolare colore. La rimozione dei sottocolori (UCR) riduce la quantità di componenti ciano, magenta e giallo per compensare la quantità di nero che la generazione di nero ha aggiunto. Poiché utilizza meno inchiostro, UCR viene generalmente utilizzato per la carta da giornale e per le scorte non rivestite.

**Quando Vengono Trovate Funzioni Di Trasferimento:** Determina cosa fare quando vengono trovate le funzioni di trasferimento:

**Mantieni:** Mantiene le funzioni di trasferimento tradizionalmente utilizzate per compensare il guadagno o la perdita di punti che possono verificarsi quando un&#39;immagine viene trasferita su pellicola. L&#39;aumento del punto si verifica quando i punti di inchiostro che compongono un&#39;immagine stampata sono più grandi (ad esempio, a causa della diffusione su carta) rispetto allo schermo di mezzitoni; la perdita del punto si verifica quando i punti vengono stampati più piccoli. Con questa opzione, le funzioni di trasferimento vengono mantenute come parte del file e applicate al file quando il file viene emesso.

**Applica:** Non mantiene la funzione di trasferimento ma la applica al file, che cambia i colori nel file. Questa opzione è utile per creare effetti di colore in un file. Per impostazione predefinita, questa opzione è selezionata per le nuove impostazioni.

**Rimuovi:** Rimuove tutte le funzioni di trasferimento applicate. Rimuovere le funzioni di trasferimento applicate a meno che il file PDF non venga inviato allo stesso dispositivo per cui è stato creato il file PostScript di origine.

**Mantieni informazioni mezzitoni:** Mantiene eventuali informazioni di mezzitoni nei file. Le informazioni di mezzitoni sono costituite da punti che controllano quanto i dispositivi di mezzitoni di inchiostro depositano in una posizione specifica sulla carta. Variando la dimensione e la densità del punto si crea l&#39;illusione di variazioni di colore grigio o continuo. Per un&#39;immagine CMYK, vengono utilizzati quattro schermi mezzitoni, uno per ogni inchiostro utilizzato nel processo di stampa.

Nella produzione di stampa tradizionale, una mezzitoni viene prodotta posizionando uno schermo mezzetinte tra un pezzo di pellicola e l&#39;immagine e poi esponendo la pellicola. Gli equivalenti elettronici, ad esempio in Adobe Photoshop, consentono agli utenti di specificare gli attributi del formato mezzetinte prima di produrre la pellicola o l&#39;uscita della carta. Le informazioni di mezzitoni sono destinate all&#39;uso con un particolare dispositivo di uscita.

## Opzioni avanzate {#advanced-options}

Le opzioni Avanzate specificano i commenti DSC (Document Structuring Conventions) da mantenere nel file PDF e come impostare altre opzioni che influiscono sulla conversione da PostScript. In un file PostScript, i commenti DSC contengono informazioni sul file (come l&#39;applicazione di origine, la data di creazione e l&#39;orientamento della pagina). Inoltre, forniscono una struttura per le descrizioni della pagina nel file (come le istruzioni iniziali e finali per una sezione prolog). I commenti DSC possono essere utili quando il documento verrà stampato o premuto. Per istruzioni su come accedere alle opzioni avanzate, consulta [Aggiungere o modificare le impostazioni di PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Quando si utilizzano le opzioni Avanzate, è utile comprendere il linguaggio PostScript e come viene tradotto in PDF. (Vedi [Adobe PostScript 3](https://www.adobe.com/products/postscript/main.html).)

**Consenti al file PostScript di ignorare le impostazioni di Adobe PDF:** Utilizza le impostazioni memorizzate in un file PostScript invece del file di impostazioni Adobe PDF corrente. Prima di elaborare un file PostScript, è possibile inserire parametri nel file per controllare i seguenti aspetti:

* compressione di testo e grafica
* decampionatura e codifica delle immagini campionate
* incorporazione di font di tipo 1 e istanze di font di tipo 1 con più principali

**Consenti oggetti XObject PostScript:** Gli oggetti XObjects PostScript memorizzano le informazioni visualizzate su molte pagine dello stesso file, ad esempio un&#39;immagine di sfondo o informazioni di intestazione e piè di pagina. L&#39;utilizzo di XObjects PostScript può causare una stampa più veloce ma richiede più memoria della stampante. Per evitare la creazione di oggetti XObjects PostScript, deselezionare questa opzione se si creano file PDF con compatibilità Acrobat 5 (PDF 1.4) o successiva.

**Converti sfumature in sfumature uniformi:** Converte le blend in sfumature uniformi per Acrobat 4 e versioni successive, riducendo i file PDF e migliorando potenzialmente la qualità dell’output finale. PDF Generator converte i gradienti da Adobe Illustrator, Adobe InDesign, Adobe FreeHand MX, CorelDraw, Quark Xpress e Microsoft PowerPoint.

**Converti linee smussate in curve:** Riduce la quantità di punti di controllo utilizzati per creare curve nei disegni CAD, il che si traduce in PDF più piccoli e rendering più veloce sullo schermo.

**Mantieni semantica pagina di copia di livello 2:** Utilizza l&#39;operatore di copypage definito nel PostScript di LanguageLevel 2 anziché nel PostScript di LanguageLevel 3. Se si dispone di un file PostScript e si seleziona questa opzione, un operatore di copypage copia la pagina. Se questa opzione non è selezionata, viene eseguito l’equivalente di un’operazione showpage, ma lo stato grafico non viene reinizializzato.

**Mantieni impostazioni di sovrastampa:** Mantiene eventuali impostazioni di sovrastampa nei file convertiti in PDF. I colori sovrastampati sono due o più inchiostri stampati uno sopra l’altro. Ad esempio, quando un inchiostro ciano stampa su un inchiostro giallo, la sovrastampa risultante è di colore verde. Senza sovrastampa, il giallo sottostante non sarebbe stampato, con conseguente colore ciano.

**L&#39;Impostazione Predefinita Per La Sovrastampa È Diversa Da Zero.** Impedisce agli oggetti sovrastampati con valori CMYK zero di eliminare gli oggetti CMYK che si trovano sotto di essi. Questo effetto viene ottenuto inserendo il parametro dello stato grafico OPM 1 nel file PDF, ovunque sia presente l’operatore Setoverprint.

**Salva le impostazioni Adobe PDF nel file PDF:** Incorpora il file delle impostazioni utilizzato per creare il file PDF. È possibile aprire e visualizzare il file delle impostazioni (che ha un&#39;estensione del nome del file .joboptions) nella finestra di dialogo File allegati in Acrobat. Il file delle impostazioni Adobe PDF diventa un elemento della struttura EmbeddedFiles all’interno del file PDF.

**Se Possibile, Salva Le Immagini JPEG Originali In PDF:** Elabora tutte le immagini compresse di JPEG (immagini già compresse utilizzando la codifica DCT) senza ricomprimerle. Se questa opzione è selezionata, PDF Generator decomprime le immagini di JPEG per assicurarsi che non siano danneggiate. Tuttavia, non ricomprime le immagini valide, pertanto l&#39;elaborazione dell&#39;immagine originale non viene modificata. Con questa opzione selezionata, le prestazioni migliorano perché si verifica solo la decompressione (non la ricompressione) e i dati immagine e metadati vengono conservati.

**Salva il ticket di lavoro portatile all’interno del file PDF:** Mantiene un ticket di lavoro PostScript in un file PDF. Il ticket di lavoro contiene informazioni sul file PostScript, ad esempio dimensioni della pagina, risoluzione e informazioni di trapping, anziché informazioni sul contenuto. Queste informazioni possono essere utilizzate in un secondo momento in un flusso di lavoro o per la stampa di PDF.

**Utilizza Prolog.ps e Epilog.ps:** Invia un file prolog ed epilog con ogni processo. Questi file hanno molti scopi. Ad esempio, è possibile modificare i file di prolog per specificare le pagine di copertina. I file Epilog possono essere modificati per risolvere una serie di procedure in un file PostScript. Puoi caricare o scaricare i file. (Vedi Caricamento e download di file prolog ed epilog.)

**Elabora commenti DSC:** Mantiene le informazioni DSC da un file PostScript. Sono disponibili le seguenti opzioni secondarie:

**Segnala avvisi DSC:** Visualizza messaggi di avviso relativi ai commenti DSC problematici durante l’elaborazione e li aggiunge a un file di registro.

**Conserva Le Informazioni Di EPS Da DSC:** Mantiene informazioni, ad esempio l’applicazione di origine e la data di creazione di un file EPS. Se questa opzione è deselezionata, la pagina viene ridimensionata e centrata in base all’angolo superiore sinistro dell’oggetto in alto a sinistra e all’angolo inferiore destro dell’oggetto in basso a destra nella pagina.

**Mantieni commenti OPI:** Mantiene le informazioni necessarie per sostituire un&#39;immagine o un commento For Placement Only (FPO) con l&#39;immagine ad alta risoluzione presente sui server che supportano le versioni 1.3 e 2.0 di Open Prepress Interface (OPI).

**Mantieni informazioni documento da DSC:** Conserva informazioni quali titolo, data e ora di creazione. Quando si apre un file PDF in Acrobat, queste informazioni vengono visualizzate nel pannello Descrizione proprietà documento .

**Ridimensiona pagina e centra immagine per file EPS:** Centra un’immagine di EPS e ridimensiona la pagina per adattarla perfettamente all’immagine. Questa opzione si applica solo ai processi costituiti da un singolo file EPS.

## Indicazioni sugli standard e opzioni di conformità {#standards-reporting-and-compliance-options}

PDF Generator può controllare il contenuto dei documenti in un file PostScript per assicurarsi che soddisfino i criteri standard PDF/X-1a, PDF/X-3 o PDF/A prima di creare il file PDF. Per i file conformi a PDF/X, è inoltre possibile richiedere che il file PostScript soddisfi criteri aggiuntivi selezionando altre opzioni in &quot;Reporting and compliance&quot; (Generazione rapporti standard e conformità). La disponibilità delle opzioni dipende dallo standard selezionato.

I file conformi a PDF/X vengono utilizzati principalmente come formato standard per lo scambio di file PDF destinati alla produzione di stampa ad alta risoluzione. A meno che non si crei un documento PDF per la produzione di stampa, è possibile ignorare gli standard di conformità PDF/X.

I file conformi a PDF/A vengono utilizzati principalmente per l’archiviazione. Poiché l&#39;obiettivo è la conservazione a lungo termine, il documento deve contenere solo ciò che è necessario per l&#39;apertura e la visualizzazione per tutta la durata prevista del documento. Ad esempio, i file conformi a PDF/A possono contenere solo testo, immagini raster e oggetti vettoriali; non possono contenere cifratura e script. Inoltre, tutti i font devono essere incorporati in modo che i documenti possano essere aperti e visualizzati come creati. In altre parole, i documenti conformi a PDF/A sono *più sottile* rispetto alle loro controparti PDF/X, destinate alla produzione high-end.

>[!NOTE]
>
>Se si imposta una cartella controllata per la creazione di file conformi a PDF/A, assicurarsi di non aggiungere protezione alla cartella; lo standard PDF/A non consente la crittografia.

Per istruzioni sull&#39;accesso alle opzioni di reporting e conformità degli standard, vedi [Aggiungere o modificare le impostazioni di PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

**Standard di conformità:** Selezionare uno standard per produrre un report che indichi se il file è conforme ai requisiti e, in caso contrario, quali problemi sono stati riscontrati. Quando Compatibilità nella pagina Impostazioni generali è impostata su Acrobat 4.0, le seguenti opzioni sono abilitate. Quando Compatibilità è impostata su Acrobat 5.0, è possibile selezionare solo le opzioni Acrobat 5.0. Quando Compatibilità è impostata su un’opzione alternativa, le opzioni seguenti sono disattivate:

* PDF/X-1a (compatibile con Acrobat 4.0)
* PDF/X-3 (compatibile con Acrobat 4.0)
* PDF/X-1a (compatibile con Acrobat 5.0)
* PDF/X-3 (compatibile con Acrobat 5.0)
* PDF/A-1b (compatibile con Acrobat 5.0)

### Opzioni per gli standard PDF/X {#options-for-pdf-x-standards}

**Se non conforme:** Specifica se creare il file PDF se il file PostScript non è conforme ai requisiti PDF/X. Questa opzione è disponibile quando Standard di conformità nella pagina Reporting and Compliance standard è impostata su un&#39;opzione diversa da Nessuno.

**Continua:** Crea un file PDF.

**Annulla processo:** Crea un file PDF solo se il file PostScript soddisfa i requisiti PDF/X delle opzioni di report selezionate ed è altrimenti valido. Se sono selezionate entrambe le opzioni del rapporto PDF/X e il file PostScript soddisfa un solo set dei criteri PDF/X (ad esempio, PDF/X-3), PDF Generator crea il file compatibile.

**Se non sono specificati TrimBox o ArtBox:** Disponibile quando Standard di conformità nella pagina Generazione rapporti e conformità standard è impostato su un&#39;opzione diversa da Nessuno.

**Segnala come errore:** Contrassegna il file PostScript come non conforme se è selezionata una delle opzioni di reporting e manca una casella di trim o una casella di disegno da qualsiasi pagina.

**Imposta TrimBox su MediaBox con offset:** Calcola i valori in punti per la casella di taglio in base agli offset per la casella del supporto delle rispettive pagine se non è specificato né il riquadro di taglio né il riquadro di disegno. La casella di trim è sempre piccola o piccola rispetto alla casella multimediale che la racchiude.

**Se BleedBox non è specificato:** Disponibile quando Standard di conformità nella pagina Generazione rapporti e conformità standard è impostato su un&#39;opzione diversa da Nessuno.

**Imposta BleedBox su MediaBox:** Utilizza i valori della casella di riepilogo per la casella di riepilogo se la casella di riepilogo non è specificata.

**Imposta BleedBox su TrimBox con offset:** Calcola i valori in punti per la casella di pagina al vivo in base agli offset per la casella di ritaglio delle rispettive pagine se la casella di pagina al vivo non è specificata. La casella di livellamento è sempre grande o più grande della casella di taglio racchiusa.

**Valori Predefiniti Se Non Specificati Nel Documento:** Questa opzione è disponibile quando Standard di conformità nella pagina Reporting and Compliance standard è impostata su un&#39;opzione diversa da Nessuno.

**Nome profilo intento di output:** Indica la condizione di stampa caratterizzata per la quale il documento è preparato. Se un documento non specifica un nome OutputIntent, PDF Generator utilizza il valore selezionato da questo menu. È possibile selezionare uno dei nomi forniti oppure immettere un nome nello spazio disponibile. Se il flusso di lavoro richiede che il documento specifichi l’intento di output, selezionare Nessuno. Qualsiasi documento che non soddisfi il requisito non supera il controllo di conformità.

**Identificatore condizione di output:** Indica il nome di riferimento specificato dal Registro di sistema del nome del profilo dell&#39;intento di output.

**Condizione di uscita:** Descrive la condizione di stampa desiderata. Questa voce può essere utile per il destinatario previsto del documento PDF.

**Nome del Registro di sistema (URL):** Indica l&#39;indirizzo Web per ulteriori informazioni sul Registro di sistema. L&#39;URL viene immesso automaticamente per i nomi del registro ICC.

**Trapping:** Indica lo stato di abbondanza nel documento. La conformità PDF/X richiede un valore True o False. Se il documento non specifica lo stato di intrappolamento, viene utilizzato il valore specificato qui. Se il flusso di lavoro richiede che il documento specifichi lo stato di intrappolamento, selezionare Lascia non definito. Qualsiasi documento che non soddisfi il requisito non supera il controllo di conformità.

### Opzioni per PDF/A standard {#options-for-pdf-a-standard}

Queste opzioni sono abilitate quando la Compatibilità (nell’area Generale) è impostata su Acrobat 4 (PDF 1.3) o Acrobat 5 (PDF 1.4).

**Se non conforme:** Specifica se creare il file PDF se il file PostScript non è conforme ai requisiti PDF/A.

**Continua:** Crea un file PDF anche se il file PostScript non soddisfa i requisiti dello standard.

**Annulla processo:** Crea un file PDF solo se il file PostScript soddisfa i requisiti PDF/A ed è altrimenti valido.

**Nome profilo intento di output:** Indica la condizione di stampa caratteristica per la quale il documento è stato preparato ed è richiesto per la conformità PDF/A. Se il flusso di lavoro richiede che il documento specifichi le informazioni sull&#39;intento di output, selezionare &quot;Nessuno&quot;. Il documento non riuscirà a controllare la conformità se queste informazioni non vengono fornite.

**Condizione di uscita:** Descrive la condizione di stampa desiderata. Questa voce non è obbligatoria, ma può essere utilizzata per fornire informazioni utili al destinatario previsto del documento PDF.

## Opzioni della vista iniziale {#initial-view-options}

Queste opzioni sono organizzate in tre aree: Opzioni documento, Opzioni finestra e Opzioni interfaccia utente. Per istruzioni su come accedere alle opzioni di visualizzazione iniziale, consulta [Aggiungere o modificare le impostazioni di PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Per utilizzare le opzioni disponibili, selezionare Imposta impostazioni visualizzazione iniziale.

### Opzioni documento {#document-options}

Le opzioni del documento controllano l&#39;aspetto del documento all&#39;interno della finestra del documento, ad esempio il livello di ingrandimento e la modalità di scorrimento.

**Mostra:** Determina i riquadri e le schede visualizzati per impostazione predefinita nella finestra dell&#39;applicazione. Il pannello Segnalibri e la pagina apre il riquadro del documento e visualizza la scheda Segnalibri.

**Layout della pagina:** Determina se il documento viene visualizzato in modalità pagina singola, pagina affiancata, pagina continua o pagina continua.

**Ingrandimento:** Imposta il livello di zoom utilizzato per visualizzare il documento quando viene aperto. Il valore predefinito utilizza il valore di ingrandimento configurato dall’utente nelle preferenze di Acrobat o Adobe Reader.

**Apri al numero di pagina:** Imposta la pagina in cui si apre il documento, che in genere è a pagina 1.

>[!NOTE]
>
>L’impostazione Predefinita per le opzioni di ingrandimento e layout di pagina utilizza le impostazioni dei singoli utenti nelle preferenze Visualizzazione pagina di Acrobat o Adobe Reader.

### Opzioni finestra {#window-options}

Le opzioni della finestra determinano il modo in cui la finestra si regola nell&#39;area dello schermo quando un utente apre il documento. Tuttavia, le opzioni non hanno alcun effetto quando un documento PDF viene visualizzato all’interno di un browser web.

**Ridimensiona finestra alla pagina iniziale:** Regola la finestra del documento in modo da adattarsi leggermente alla pagina di apertura, in base alle opzioni selezionate in Opzioni documento.

**Finestra centrale sullo schermo:** Posiziona la finestra al centro dell&#39;area dello schermo.

**Apri In Modalità A Schermo Intero:** Ingrandisce la finestra del documento e visualizza il documento senza i controlli della barra dei menu, della barra degli strumenti o della finestra.

**Mostra:** Il nome file mostra il nome del file nella barra del titolo della finestra. Il titolo del documento mostra il titolo del documento nella barra del titolo della finestra.

### Opzioni dell’interfaccia utente {#user-interface-options}

Le opzioni dell’interfaccia utente determinano quali controlli vengono visualizzati o nascosti quando l’utente apre il documento.

**Nascondi barra dei menu:** Se selezionata, nasconde la barra dei menu

**Nascondi barre degli strumenti:** Se selezionata, nasconde le barre degli strumenti

**Nascondi controlli finestra:** Se selezionata, nasconde i controlli della finestra

>[!NOTE]
>
>Se nascondi la barra dei menu e la barra degli strumenti, gli utenti non possono applicare comandi e selezionare strumenti a meno che non conoscano le scelte rapide da tastiera all’apertura del file in Acrobat.

## Caricamento e download di file prolog ed epilog {#uploading-and-downloading-prologue-and-epilogue-files}

I file di registro vengono utilizzati per aggiungere codice PostScript personalizzato che viene eseguito all&#39;inizio di ogni processo PostScript in fase di distillazione. I file Epilog vengono utilizzati per aggiungere codice PostScript personalizzato che viene eseguito alla fine di ogni processo PostScript. È possibile scaricare i file prolog ed epilog dal server per salvarli localmente. È possibile scaricare i file per configurarli in modo indipendente o per caricarli in un altro percorso o in un altro computer.

Questi file hanno molti scopi. Ad esempio, è possibile modificare i file di profilo per specificare le pagine di copertina; I file epilog possono essere modificati per risolvere una serie di procedure in un file PostScript. Puoi anche selezionare e caricare i file prolog ed epilog da inviare con ogni lavoro.

### Scaricare un file prolog o epilog {#download-a-prologue-or-epilogue-file}

1. Nella console di amministrazione, fai clic su Servizi > Generatore PDF > Impostazioni Adobe PDF.
1. Fare clic su Nuovo o sul nome di un&#39;impostazione.
1. Fare clic su Avanzate e quindi, accanto all&#39;opzione Usa Prolog.ps e Epilog.ps, fare clic su Scarica.
1. Nella pagina Scarica file Prolog ed Epilog, fai clic su Prolog.ps o Epilog.ps e fai clic su Salva.

### Caricare un file prolog o epilog {#upload-a-prologue-or-epilogue-file}

1. Nella console di amministrazione, fai clic su Servizi > Generatore PDF > Impostazioni Adobe PDF.
1. Fare clic su Nuovo o sul nome di un&#39;impostazione.
1. Fai clic su Avanzate e quindi, accanto all’opzione Usa Prolog.ps e Epilog.ps, fai clic su Carica.
1. Nella pagina Carica file prolog ed Epilog, fai clic su Sfoglia per selezionare un file prolog o epilog.
1. Individuare il file e fare clic su Apri.
1. Per utilizzare il file , accertati che Use Prolog.ps And Epilog.ps sia selezionato nell&#39;area Avanzate della pagina Nuova/Modifica impostazione Adobe PDF .
1. Fai clic su Salva

>[!NOTE]
>
>PDF Generator supporta i file prolog ed epilog solo per la conversione di file PostScript e PostScript incapsulati in PDF.
