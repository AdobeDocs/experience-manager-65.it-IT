---
title: Configurazione delle impostazioni di Adobe PDF
description: Scopri come configurare le impostazioni Adobe PDF visibili nella pagina Impostazioni Adobe PDF. Puoi utilizzare una qualsiasi delle impostazioni predefinite di PDF o crearne di personalizzate.
uuid: 980c9d6a-f75e-4e7d-b050-d2d07a10ef33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab018b6d-0233-4439-bb75-58c5421d769a
feature: PDF Generator
exl-id: 1bcb8429-c06e-4bd3-b422-4c512084dd09
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '7285'
ht-degree: 0%

---

# Configurazione delle impostazioni di Adobe PDF{#configuring-adobe-pdf-settings}

La pagina Impostazioni di Adobe PDF mostra le impostazioni di conversione che è possibile specificare per le origini da utilizzare. Puoi utilizzare una qualsiasi delle impostazioni predefinite di PDF o crearne di personalizzate. Le impostazioni di PDF determinano con precisione la modalità di conversione dei file e la struttura e le funzionalità PDF risultanti. Le impostazioni di Adobe PDF erano precedentemente note come parametri di Distiller® o opzioni di processo.

Nella pagina Impostazioni di Adobe PDF puoi effettuare le seguenti operazioni:

* Visualizzare le impostazioni predefinite di PDF. (vedere [Informazioni sulle impostazioni predefinite di PDF](configuring-pdf-settings.md#about-the-predefined-pdf-settings).)
* Creare un&#39;impostazione di PDF o modificarne una creata in precedenza. (vedere [Aggiungi o modifica impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).)
* Specificare le impostazioni predefinite di PDF. (vedere [Modificare le impostazioni predefinite](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings))
* Carica un file di impostazioni PDF sul server. (vedere [Carica impostazioni PDF](configuring-pdf-settings.md#upload-pdf-settings).)
* Elimina le impostazioni personalizzate di PDF. (vedere [Elimina impostazioni PDF](configuring-pdf-settings.md#delete-pdf-settings).)
* Carica e scarica i file prolog ed epilog. (vedere [Caricamento e download di file prolog ed epilog](configuring-pdf-settings.md#uploading-and-downloading-prologue-and-epilogue-files).)

Le impostazioni Adobe PDF sono applicabili solo alle conversioni basate su PDFMaker. Queste includono le seguenti conversioni:

* Documento Microsoft Word (DOC, DOCX, RTF, TXT)
* Documento Microsoft Excel (XLS, XLSX)
* Documento di Microsoft PowerPoint (PPT, PPTX)
* Documento progetto Microsoft (MPP)
* Documento di Microsoft Visio (VSD)

>[!NOTE]
>
>Quando si utilizza OpenOffice per convertire i formati precedenti, le impostazioni Adobe PDF non vengono applicate.

## Informazioni sulle impostazioni predefinite di PDF {#about-the-predefined-pdf-settings}

PDF Generator fornisce diverse impostazioni PDF predefinite per il tuo utilizzo. Non è possibile modificare queste impostazioni predefinite; tuttavia, è possibile creare un&#39;impostazione basata su una esistente modificandola e salvandola con un nuovo nome.

**Stampa di alta qualità:** Crea file PDF per output di alta qualità. Questa impostazione:

* downsampling di immagini a colori e in scala di grigio a 300 dpi
* downsampling immagini monocromatiche a 1200 dpi
* stampa a una risoluzione immagine più elevata
* utilizza altre impostazioni per mantenere la quantità massima di informazioni sul documento originale.

Questi file PDF possono essere aperti in Adobe Acrobat 5 e Adobe Acrobat Reader® 5 o versioni successive.

**Pagine di dimensioni eccessive:** Consente di creare documenti PDF adatti alla visualizzazione e alla stampa affidabili di disegni tecnici di dimensioni superiori a 200 x 200 pollici. I documenti PDF creati possono essere aperti in Adobe Acrobat Professional e Acrobat Standard, versione 7 o successiva, e Adobe Reader 7 o versione successiva.

**PDF/A-1B 2005 CMYK/PDF/A-1B 2005 RGB:** Verifica la conformità dei processi in arrivo allo standard ISO per la conservazione a lungo termine (archiviazione) dei documenti elettronici e crea file PDF/A solo se conformi. Questi file vengono utilizzati principalmente per l&#39;archiviazione. I file conformi possono contenere solo testo, immagini raster e oggetti vettoriali; non possono contenere crittografia e script. Inoltre, tutti i font devono essere incorporati in modo che i documenti possano essere aperti e visualizzati come creati. PDF/A-1b utilizza PDF 1.4 e converte tutti i colori in CMYK o RGB, a seconda dello standard scelto. I file PDF creati con questo file di impostazioni possono essere aperti in Acrobat 5 e Acrobat Reader 5 e versioni successive. Per ulteriori informazioni su PDF/A, consulta l’Adobe e gli standard di settore.

**PDF/X-1a 2001:** Verifica la conformità dei processi in ingresso a PDF/X-1a e crea i file PDF solo se conformi. PDF/X-1a è uno standard ISO per lo scambio di contenuti grafici. PDF/X-1a richiede l&#39;incorporamento di tutti i font, la specifica delle caselle di PDF appropriate e la visualizzazione del colore come colori CMYK o tinta piatta. I file PDF che soddisfano i requisiti PDF/X-1a sono destinati a una condizione di output specifica, ad esempio la stampa offset Web in base alle specifiche Web Offset Publications. Per ulteriori informazioni su PDF/X, consulta l’Adobe e gli standard di settore.

**PDF/X-3 2002:** Verifica la conformità dei processi in ingresso a PDF/X-3 e crea i file PDF solo se conformi. Come PDF/X-1a, PDF/X-3 è uno standard ISO per lo scambio di contenuti grafici. La differenza principale è che PDF/X-3 supporta colori indipendenti dal dispositivo.

**Qualità stampa:** Crea file PDF per la produzione di stampe di alta qualità, ad esempio su fotounità o piastrine. In questo caso, la dimensione del file non viene presa in considerazione. L&#39;obiettivo è quello di conservare tutte le informazioni contenute in un file PDF necessarie a un servizio di stampa esterno o a un fornitore di servizi di prestampa per stampare correttamente il documento. Questa serie di opzioni:

* downsampling di immagini a colori e in scala di grigio a 300 dpi
* downsampling immagini monocromatiche a 1200 dpi
* incorpora sottoinsiemi di tutti i font utilizzati nel documento
* stampa ad una risoluzione più elevata,
* non ruota automaticamente le pagine in base all&#39;orientamento dei commenti DSC (Document Structuring Convention)
* utilizza altre impostazioni per mantenere la quantità massima di informazioni sul documento originale.

I processi di stampa hanno esito negativo se dispongono di tipi di carattere che non possono essere incorporati. Questi file PDF possono essere aperti in Acrobat 5 e Acrobat Reader 5 e versioni successive.

>[!NOTE]
>
>Prima di creare un file PDF da inviare a un servizio di stampa esterno o a un provider di servizi di prestampa, determinare la risoluzione di output e altre impostazioni oppure richiedere un file joboptions con le impostazioni consigliate. Potrebbe essere necessario personalizzare le impostazioni di Adobe PDF per un determinato provider e quindi fornire un file .joboptions personalizzato.

**Dimensione file minima:** Crea file PDF da visualizzare sul Web o su una rete Intranet oppure da distribuire tramite un sistema e-mail per la visualizzazione sullo schermo. Questa serie di opzioni utilizza la compressione, il downsampling e una risoluzione dell&#39;immagine relativamente bassa. Converte tutti i colori in sRGB e non incorpora i font se non necessario. Inoltre, ottimizza i file per la distribuzione dei byte. Questi file PDF possono essere aperti in Acrobat 5 e Acrobat Reader 5.0 e versioni successive.

**Standard:** Crea file PDF da stampare su stampanti desktop o fotocopiatrici digitali, pubblicare su CD o inviare a un client come bozza di pubblicazione. Questa serie di opzioni utilizza la compressione e il downsampling per ridurre le dimensioni del file. Incorpora inoltre sottoinsiemi di tutti i font utilizzati nel file, converte tutti i colori in sRGB e stampa a una risoluzione media per creare una rappresentazione ragionevolmente accurata del documento originale. I sottoinsiemi di caratteri di Microsoft Windows non sono incorporati per impostazione predefinita. Questi file PDF possono essere aperti in Acrobat 5 e Acrobat Reader 5.0 e versioni successive.

## Aggiungi o modifica impostazioni PDF {#add-or-edit-pdf-settings}

Le impostazioni di PDF determinano con precisione il modo in cui i file vengono convertiti e la struttura e le funzionalità PDF risultanti. Definisci una nuova impostazione di PDF o modificane una creata in precedenza. Non è possibile modificare le impostazioni predefinite, ma è possibile creare un&#39;impostazione basata su una esistente modificandola e salvandola con un nuovo nome.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Impostazioni Adobe PDF.
1. Fare clic su Nuovo o sul nome di un&#39;impostazione esistente.
1. Nella pagina Nuova/Modifica impostazione Adobe PDF, inserisci le informazioni richieste nelle sezioni seguenti:

[Opzioni generali](configuring-pdf-settings.md#general-options)

[Opzioni immagini](configuring-pdf-settings.md#images-options)

[Opzioni font](configuring-pdf-settings.md#fonts-options)

[Opzioni colore](configuring-pdf-settings.md#color-options)

[Opzioni avanzate](configuring-pdf-settings.md#advanced-options)

[Report standard e opzioni di conformità](configuring-pdf-settings.md#standards-reporting-and-compliance-options)

[Opzioni di visualizzazione iniziale](configuring-pdf-settings.md#initial-view-options)

   Per passare a un&#39;altra sezione, fare clic sul relativo collegamento nella pagina Web oppure utilizzare i pulsanti Successivo e Precedente.

1. Dopo aver completato le informazioni in tutte le sezioni, fare clic su Salva o Salva con nome e specificare un nome per l&#39;impostazione.

## Carica impostazioni PDF {#upload-pdf-settings}

Le impostazioni di PDF possono essere disponibili nel server PDF Generator caricandole da un computer locale o da un percorso di rete.

1. In Administration Console, fai clic su Servizi > PDF Generator > Impostazioni Adobe PDF, quindi fai clic su Carica.
1. Nella pagina Carica impostazioni Adobe PDF fare clic su Sfoglia, individuare il file delle impostazioni di PDF e fare clic su Apri.
1. Fare clic su OK e quindi di nuovo su OK.

## Elimina impostazioni PDF {#delete-pdf-settings}

Se non sono più necessarie, è possibile eliminare definitivamente le impostazioni di PDF.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Impostazioni Adobe PDF.
1. Selezionare la casella di controllo accanto all&#39;impostazione da eliminare. È possibile selezionare più impostazioni.
1. Fare clic su Elimina e quindi di nuovo su Elimina nella pagina Conferma eliminazione.

## Opzioni generali {#general-options}

Utilizza le opzioni generali per specificare la versione di Acrobat da utilizzare per la compatibilità dei file e altre opzioni per file e dispositivi. Per istruzioni sull&#39;accesso alle opzioni generali, vedere [Aggiungi o modifica impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Opzioni file {#file-options}

**Compatibilità:** Livello di compatibilità del file PDF. Per i documenti che verranno distribuiti in modo ampio, è consigliabile selezionare Acrobat 4 (PDF 1.3) o Acrobat 5 (PDF 1.4) per garantire che tutti gli utenti possano visualizzare e stampare il documento. Se crei file utilizzando la compatibilità Acrobat 5 o versione successiva, questi potrebbero non essere compatibili con le versioni precedenti di Acrobat. Le sottosezioni seguenti mostrano alcune delle differenze tra i file PDF creati utilizzando diversi livelli di compatibilità di Acrobat.

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
   <td><p>Può essere aperto con Acrobat 3.0 e Acrobat Reader 3.0 e versioni successive. Le funzioni specifiche delle versioni successive potrebbero andare perse o non essere visualizzabili.</p> </td>
   <td><p>La maggior parte può essere aperta con Acrobat 4 e Acrobat Reader 4.0 e versioni successive. Le funzioni specifiche delle versioni successive potrebbero andare perse o non essere visualizzabili.</p> </td>
   <td><p>La maggior parte può essere aperta con Acrobat 4 e Acrobat Reader 4.0 e versioni successive. Le funzioni specifiche delle versioni successive potrebbero andare perse o non essere visualizzabili.</p> </td>
  </tr>
  <tr>
   <td><p>Non può contenere immagini che utilizzano effetti di trasparenza attivi. Qualsiasi trasparenza deve essere appiattita prima della conversione in PDF 1.3.</p> </td>
   <td><p>Supporta l'utilizzo della trasparenza in tempo reale nelle immagini. La funzione Acrobat Distiller appiattisce la trasparenza.</p> </td>
   <td><p>Supporta l'utilizzo della trasparenza in tempo reale nelle immagini. La funzione Acrobat Distiller appiattisce la trasparenza.</p> </td>
   <td><p>Supporta l'utilizzo della trasparenza in tempo reale nelle immagini. La funzione Acrobat Distiller appiattisce la trasparenza.</p> </td>
  </tr>
  <tr>
   <td><p>I livelli non sono supportati.</p> </td>
   <td><p>I livelli non sono supportati.</p> </td>
   <td><p>Mantiene i livelli quando si creano file PDF da applicazioni che supportano la generazione di documenti PDF con livelli, ad esempio Adobe Illustrator® CS o Adobe InDesign® CS e versioni successive.</p> </td>
   <td><p>Mantiene i livelli quando si creano file PDF da applicazioni che supportano la generazione di documenti PDF con livelli, ad esempio Illustrator CS o InDesign CS e versioni successive.</p> </td>
  </tr>
  <tr>
   <td><p>È supportato lo spazio colore DeviceN con 8 coloranti.</p> </td>
   <td><p>È supportato lo spazio colore DeviceN con 8 coloranti.</p> </td>
   <td><p>È supportato lo spazio colore DeviceN con un massimo di 31 coloranti.</p> </td>
   <td><p>È supportato lo spazio colore DeviceN con un massimo di 31 coloranti.</p> </td>
  </tr>
  <tr>
   <td><p>È possibile incorporare caratteri multibyte. (Distiller converte i font durante l'incorporamento).</p> </td>
   <td><p>È possibile incorporare caratteri multibyte.</p> </td>
   <td><p>È possibile incorporare caratteri multibyte.</p> </td>
   <td><p>È possibile incorporare caratteri multibyte.</p> </td>
  </tr>
  <tr>
   <td><p>È supportata la sicurezza RC4 a 40 bit.</p> </td>
   <td><p>È supportata la sicurezza RC4 a 128 bit.</p> </td>
   <td><p>È supportata la sicurezza RC4 a 128 bit.</p> </td>
   <td><p>Supporto della protezione RC4 a 128 bit e AES (Advanced Encryption Standard) a 128 bit.</p> </td>
  </tr>
 </tbody>
</table>

**Compressione livello oggetto:** Consolida gli oggetti di piccole dimensioni (ciascuno dei quali non è comprimibile) in flussi che possono essere compressi in modo efficiente.

**Disattivato:** Non comprime alcuna informazione strutturale nel documento di PDF. Selezionare questa opzione se si desidera che gli utenti visualizzino, esplorino e interagiscano con segnalibri e altre informazioni strutturali utilizzando Acrobat 5 e versioni successive.

**Solo tag:** Comprime le informazioni strutturali nel documento di PDF. L’utilizzo di questa opzione determina un file PDF che può essere aperto e stampato utilizzando Acrobat 5. Gli utenti non possono visualizzare informazioni su accessibilità, struttura o PDF con tag in Acrobat 5 o Acrobat Reader 5.0, ma possono visualizzarle in Acrobat 6 e Adobe Reader 6.0.

**Ruota automaticamente pagine:** Imposta la rotazione automatica delle pagine in base all&#39;orientamento del testo o dei commenti DSC. Ad esempio, alcune pagine (come quelle contenenti tabelle) possono richiedere all’utente di ruotarle lateralmente per leggerle. Selezionare Singolarmente per ruotare ogni pagina in base alla direzione del testo sulla pagina. Selezionare Collettivo per file per ruotare tutte le pagine del documento in base all&#39;orientamento della maggior parte del testo.

>[!NOTE]
>
>Se l&#39;opzione Elabora commenti DSC è selezionata nelle impostazioni avanzate e sono inclusi i commenti di %%Orientamento visualizzazione, questi hanno la precedenza nella determinazione dell&#39;orientamento della pagina.

**Binding:** Specifica se visualizzare un file PDF con associazione a sinistra o a destra. Questa impostazione ha effetto sulla visualizzazione delle pagine nel layout Pagina faccia - continua e la visualizzazione delle miniature affiancata.

**Risoluzione:** Imposta l&#39;emulazione per la risoluzione di una stampante per i file di input che ne regolano il comportamento in base alla risoluzione della stampante su cui vengono stampati. Per la maggior parte dei file di input, un&#39;impostazione con una risoluzione più elevata genera file PDF di dimensioni maggiori ma di qualità superiore, mentre un&#39;impostazione più bassa genera file PDF di dimensioni minori ma di qualità inferiore. Nella maggior parte dei casi, la risoluzione determina il numero di passi di una sfumatura o di una fusione. È possibile immettere un valore compreso tra 72 e 4000. Mantenere questa impostazione come predefinita a meno che non si intenda stampare il file PDF su una stampante specifica e si desideri emulare la risoluzione definita nel file di input originale.

>[!NOTE]
>
>L&#39;aumento dell&#39;impostazione di risoluzione aumenta le dimensioni dei file e può aumentare leggermente il tempo necessario per elaborare alcuni file.

**Tutte le pagine o pagine da:** Specifica le pagine da convertire. Lasciare vuota la casella A per creare un intervallo dal numero di pagina immesso nella casella Da alla fine del file.

**Ottimizza Per Visualizzazione Web Veloce:** Consente di ristrutturare il file per il download di una pagina alla volta (byte serving) dai server Web. Questa opzione comprime il testo e la grafica a linee, indipendentemente dalle impostazioni di compressione selezionate nella scheda Immagini. La compressione consente un accesso e una visualizzazione più rapidi durante il download del file dal web o da una rete. Per impostazione predefinita, questa opzione non è abilitata.

### Dimensioni pagina predefinite {#default-page-size}

Le opzioni Dimensioni pagina predefinite specificano la dimensione della pagina da utilizzare quando non è specificata nel file originale. In genere, i file di Adobe PostScript includono queste informazioni, ad eccezione dei file PostScript incapsulati (EPS), che danno una dimensione del riquadro ma non una dimensione della pagina. La dimensione massima consentita per la pagina è di 31.800.000 cm in entrambe le direzioni. Queste opzioni configurano le dimensioni di pagina predefinite:

**Larghezza:** Larghezza della pagina

**Altezza:** Altezza della pagina

**Unità:** Unità da utilizzare per le impostazioni di larghezza e altezza

## Opzioni immagini {#images-options}

Le opzioni Immagini specificano la compressione e il ricampionamento delle immagini. Potete sperimentare queste opzioni per trovare un giusto equilibrio tra le dimensioni del file e la qualità dell&#39;immagine. Per istruzioni sull&#39;accesso alle impostazioni delle immagini, vedere [Aggiungi o modifica impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Queste opzioni configurano le immagini a colori, in scala di grigio e monocromatiche:

**Downsampling:** Imposta un valore per ogni tipo di immagine. Per eseguire il downsampling di immagini a colori, in scala di grigio o monocromatiche, PDF Generator combina i pixel in un&#39;area campione per ingrandire un pixel. Fornite la risoluzione del dispositivo di output in punti per pollice (dpi) e immettete una risoluzione in dpi nella casella Per immagini (For Images) sopra. Per le immagini con una risoluzione superiore a questa soglia, PDF Generator combina i pixel necessari per ridurre la risoluzione dell&#39;immagine (pixel per pollice) all&#39;impostazione dpi specificata. Per disattivare il downsampling, selezionare Disattivato. Di seguito sono riportate le opzioni disponibili:

**Downsampling medio per:** Calcola la media dei pixel in un&#39;area campione e sostituisce l&#39;intera area con il colore pixel medio alla risoluzione specificata.

**Downsampling Bicubico per:** Utilizza una media ponderata per determinare il colore dei pixel e di solito produce risultati migliori rispetto al semplice metodo di calcolo della media per il downsampling. Il bicubico è il metodo più lento ma preciso e produce gradazioni tonali più uniformi.

**Sottocampionamento a:** Seleziona un pixel al centro dell&#39;area di campionamento e sostituisce l&#39;intera area con tale pixel alla risoluzione specificata. Il sottocampionamento riduce in modo significativo il tempo di conversione rispetto al sottocampionamento, ma produce immagini meno uniformi e continue.

L&#39;impostazione della risoluzione per il colore e la scala di grigi deve essere compresa tra 1,5 e 2 volte la risoluzione dello schermo a cui verrà stampato il file. (Se non si va al di sotto di questa impostazione di risoluzione consigliata, le immagini che non contengono linee rette o motivi geometrici o ripetuti non vengono influenzate da una risoluzione inferiore.) La risoluzione per le immagini monocromatiche deve essere la stessa del dispositivo di output. Tuttavia, il salvataggio di un&#39;immagine monocromatica a una risoluzione superiore a 1500 dpi aumenta le dimensioni del file senza migliorare sensibilmente la qualità dell&#39;immagine.

Inoltre, considera se gli utenti devono ingrandire una pagina. Ad esempio, se stai creando un documento PDF di una mappa, puoi utilizzare una risoluzione immagine più alta in modo che gli utenti possano ingrandire la mappa.

>[!NOTE]
>
>Il ricampionamento delle immagini monocromatiche può produrre risultati di visualizzazione imprevisti, ad esempio la mancata visualizzazione delle immagini. Se si verifica questo problema, disattivare il ricampionamento e convertire di nuovo il file. Questo problema si verifica con maggiore probabilità con il sottocampionamento e con minore probabilità con il sottocampionamento bicubico.

Questa tabella mostra i tipi di stampanti e la loro risoluzione misurata in dpi, la loro linea dello schermo predefinita misurata in linee per pollice (lpi) e una risoluzione di ricampionamento per le immagini misurate in pixel per pollice (ppi). Ad esempio, per stampare su una stampante laser a 600 dpi, immettere 170 per la risoluzione in cui ricampionare le immagini.

<table>
 <tbody>
  <tr>
   <th><p>Risoluzione della stampante</p> </th>
   <th><p>Schermata di riga predefinita</p> </th>
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

**Compressione:** Imposta un valore da applicare alle immagini a colori, in scala di grigio e monocromatiche. Per le immagini a colori e in scala di grigi, impostare anche la qualità dell&#39;immagine:

* Per le immagini a colori o in scala di grigi, selezionare ZIP per applicare la compressione che funziona bene sulle immagini con grandi aree di singoli colori o motivi ripetuti. Alcuni esempi sono le schermate, le immagini semplici create con programmi di disegno e le immagini monocromatiche che contengono modelli ripetuti. Selezionare JPEG, da qualità minima a massima, per applicare una compressione adatta alle immagini in scala di grigi o a colori, ad esempio fotografie a tonalità continue contenenti più dettagli di quelli riproducibili sullo schermo o in stampa. Selezionare Automatico (JPEG) per determinare automaticamente la qualità migliore per le immagini a colori e in scala di grigio.
* Per le immagini monocromatiche, selezionate CCITT Group 4, CCITT Group 3, ZIP, JPEG200, Automatic (JPEG2000) o Run Length.

Assicurarsi che le immagini monocromatiche vengano acquisite come monocromatiche e non come gradazioni di grigio. Per impostazione predefinita, il testo digitalizzato viene talvolta salvato come immagini in scala di grigio. Il testo in scala di grigio compresso con il metodo di compressione JPEG non è chiaro e potrebbe essere illeggibile.

**Qualità immagine:** Configura la qualità delle immagini a colori e in scala di grigi. Le opzioni sono Minimo, Basso, Medio, Alto e Massimo.

**Antialias a grigio:** Smussa i bordi frastagliati nelle immagini monocromatiche. Selezionare 2 bit, 4 bit o 8 bit per specificare 4, 16 o 256 livelli di grigio. (L&#39;anti-aliasing può offuscare il tipo piccolo o le linee sottili).

>[!NOTE]
>
>La compressione del testo e della grafica è sempre attiva.

**Criterio immagine:** Imposta un criterio per le immagini a colori, in scala di grigio e monocromatiche. Se la risoluzione dell&#39;immagine scende al di sotto della risoluzione specificata, è comunque possibile scegliere di procedere (Ignora), inviare un messaggio di avviso o annullare il processo.

## Opzioni font {#fonts-options}

Le opzioni Tipi di carattere specificano i tipi di carattere da incorporare in un file PDF e se incorporare un sottoinsieme di caratteri utilizzati nel file PDF. Per istruzioni sull&#39;accesso alle opzioni relative ai caratteri, vedere [Aggiungi o modifica impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

>[!NOTE]
>
>Quando combinate file PDF con lo stesso sottoinsieme di caratteri, PDF Generator tenta di combinare i sottoinsiemi di caratteri.

**Incorpora tutti i font:** Incorpora tutti i font utilizzati nel file. L’incorporamento dei caratteri è necessario per garantire la conformità di PDF/X.

**Sottoinsieme Di Caratteri Incorporati Quando La Percentuale Di Caratteri Utilizzati È Inferiore A:** Se selezionate questa opzione, specificate una percentuale di soglia per incorporare solo un sottoinsieme dei font. Ad esempio, se la soglia è 35 e viene utilizzato meno del 35% dei caratteri, PDF Generator incorpora solo tali caratteri. Sono incorporati solo i font con i bit di autorizzazione appropriati.

**Quando l’incorporamento non riesce:** Specifica la modalità di risposta di PDF Generator se non è in grado di trovare un carattere da incorporare durante l&#39;elaborazione di un file. È possibile fare in modo che PDF Generator ignori la richiesta e sostituisca il tipo di carattere, invii un avviso e sostituisca il tipo di carattere oppure annulli l&#39;elaborazione del processo corrente.

**Origine font:** Posizione dei font utilizzati da PDF Generator.

### Specificare i font da incorporare {#specify-which-fonts-to-embed}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Impostazioni Adobe PDF.
1. Fai clic su Nuovo o sul nome di un’impostazione.
1. Fare clic su Tipi di carattere e deselezionare Incorpora tutti i tipi di carattere.
1. Nell&#39;elenco Origine font selezionare un&#39;origine font e fare clic su Vai per aggiornare l&#39;elenco dei font nella casella a sinistra.
1. Fare clic su un tipo di carattere nella casella a sinistra. Quindi fare clic su Aggiungi accanto alla casella appropriata per spostarlo nell&#39;elenco Incorpora sempre o Mai incorporare. Ripetere l&#39;operazione per ogni tipo di carattere. Premete Ctrl e fate clic per selezionare più font da spostare.
1. Per rimuovere un carattere dall&#39;elenco Incorpora sempre o Non incorporare mai, selezionarlo e fare clic su Rimuovi accanto alla casella appropriata. Questa azione non rimuove il font dal sistema, ma semplicemente rimuove il relativo riferimento nell&#39;elenco.
1. Se il tipo di carattere che si desidera specificare non viene visualizzato, digitarne il nome nella casella Aggiungi carattere e quindi fare clic su Incorpora sempre o Non incorporare mai. I nomi dei caratteri non possono contenere caratteri alfanumerici.

>[!NOTE]
>
>Un tipo di carattere TrueType può contenere un&#39;impostazione aggiunta dal progettista del tipo di carattere che impedisce l&#39;incorporamento del tipo di carattere nei file PDF.

>[!NOTE]
>
>I font vengono selezionati dalla cache dei font del sistema Windows ed è necessario riavviare il sistema per aggiornare la cache. Dopo aver specificato la directory dei caratteri del cliente, assicurarsi di riavviare il sistema in cui sono installati i moduli AEM.

## Opzioni colore {#color-options}

Le opzioni Colore impostano tutte le informazioni di gestione colore per PDF Generator. Per istruzioni sull&#39;accesso alle opzioni Colore, consultate [Aggiungi o modifica impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Impostazioni Adobe Color {#adobe-color-settings}

**File impostazioni:** Questo elenco contiene un elenco di impostazioni dei colori utilizzate anche nelle principali applicazioni grafiche, come Adobe Photoshop e Adobe Illustrator. L&#39;impostazione del colore selezionata determina le altre impostazioni del colore di Adobe in questa pagina. Ad esempio, se selezioni un’impostazione diversa da Nessuno, tutte le opzioni diverse da quelle per Dati dipendenti dal dispositivo sono predefinite e disabilitate. È possibile modificare le impostazioni di Criteri gestione colore e Spazi di lavoro solo se si seleziona Nessuno per File impostazioni.

### Criteri di gestione colore {#color-management-policies}

Se è stato selezionato Nessuno per il file delle impostazioni, l&#39;area Criteri di gestione colore specifica in che modo PDF Generator converte i colori non gestiti in un file PostScript.

**Lascia il colore invariato:** Lascia invariati i colori dipendenti dal dispositivo e mantiene i colori indipendenti dal dispositivo come il più vicino equivalente possibile in PDF. Questa opzione è utile per stampare i negozi che hanno calibrato tutti i loro dispositivi, hanno utilizzato tali informazioni per specificare il colore nel file e l&#39;output solo su tali dispositivi.

**Assegna tag a tutto per la gestione del colore:** Incorpora un profilo International Color Consortium durante la distillazione dei file e la calibrazione del colore nelle immagini, rendendo i colori nei file PDF risultanti indipendenti dal dispositivo se è stata selezionata la compatibilità con Acrobat 4 (PDF 1.3) o versioni successive. Tuttavia, gli spazi colore dipendenti dalla periferica nei file (RGB, Scala di grigio e CMYK) vengono convertiti in spazi colore indipendenti dalla periferica (CalRGB, CalGray e LAB).

**Tag solo immagini per gestione colore:** Incorpora i profili ICC solo nelle immagini, non nel testo o nella grafica, durante la distillazione dei file, se è stata selezionata la compatibilità con Acrobat 4 (PDF 1.3). Questa opzione impedisce al testo nero di subire uno spostamento di colore. Tuttavia, gli spazi colore dipendenti dalla periferica nelle immagini (RGB, Scala di grigio e CMYK) vengono convertiti in spazi colore indipendenti dalla periferica (CalRGB, CalGray e LAB). Testo e grafica non vengono convertiti.

**Converti tutti i colori in sRGB o Converti tutti i colori in CMYK:** Calibra il colore nel file, rendendo il colore indipendente dalla periferica, in modo simile a Tag Everything for Color Management. Se avete selezionato Compatibilità Acrobat 4 (PDF 1.3) o versione successiva e convertite in sRGB, le immagini CMYK e RGB vengono convertite in sRGB.

Indipendentemente dall&#39;opzione di compatibilità selezionata, le immagini in scala di grigio vengono lasciate invariate. Questo di solito riduce le dimensioni e aumenta la velocità di visualizzazione dei file PDF perché sono necessarie meno informazioni per descrivere le immagini RGB rispetto alle immagini CMYK. Poiché RGB è lo spazio colore nativo utilizzato sui monitor, non è necessaria alcuna conversione del colore durante la visualizzazione, contribuendo ad accelerare la visualizzazione online. Questa opzione è consigliata se il file PDF è da utilizzare online o con stampanti a bassa risoluzione.

**Intento di rendering documento:** Metodo per la mappatura dei colori tra spazi di colore. Il risultato di un particolare metodo dipende dai profili degli spazi di colore. Ad esempio, alcuni profili producono risultati identici con metodi diversi. Sono disponibili le seguenti opzioni:

>[!NOTE]
>
>In tutti i casi, gli intenti possono essere ignorati o sovrascritti dalle operazioni di gestione del colore che si verificano dopo la creazione del file PDF.

**Mantieni:** Indica che l’intento è specificato nel dispositivo di output anziché nel file PDF. In molti dispositivi di output, l&#39;intento predefinito è Colorimetrico relativo.

**Percettivo:** Mantiene i valori di colore relativi tra i pixel originali così come sono mappati alla gamma di destinazione. Questo metodo mantiene la relazione visiva tra i colori, anche se i valori dei colori stessi possono cambiare.

**Saturazione:** Mantiene i valori di saturazione relativi dei pixel originali. Questo metodo è adatto per la grafica aziendale, in cui la relazione esatta tra i colori non è importante quanto avere colori saturi brillanti.

**Colorimetrico relativo:** Rimappone il punto bianco dello spazio di origine al punto bianco dello spazio di destinazione.

**Colorimetrico assoluto:** Disattiva la corrispondenza tra punti bianchi e neri durante la conversione dei colori. Questo metodo non è consigliato, a meno che non sia necessario mantenere i colori della firma, ad esempio quelli utilizzati nei marchi o nei loghi.

### Spazi di lavoro {#working-spaces}

Per tutti i valori dell&#39;elenco in Criteri di gestione colore, ad eccezione di Lascia colore invariato, selezionare gli elenchi nell&#39;area Area di lavoro per specificare quali profili ICC vengono utilizzati per definire e calibrare gli spazi colore RGB, CMYK e scala di grigi nei file PDF distillati. Sono disponibili le seguenti opzioni:

**Grigio:** Definisce lo spazio colore di tutte le immagini in scala di grigio nei file. Questa opzione è disponibile solo se avete scelto Assegna tag a tutto per Gestione colore o Assegna tag solo alle immagini per Gestione colore. Il profilo ICC predefinito per le immagini grigie è Grey Gamma 2.2. È inoltre possibile selezionare Nessuno per impedire la conversione delle immagini in scala di grigio.

**RGB:** Definisce lo spazio colore di tutte le immagini RGB nei file. L&#39;impostazione predefinita, sRGB IEC61966-2.1, è in genere una buona scelta perché sta diventando uno standard di settore e molti dispositivi di uscita lo riconoscono. È inoltre possibile selezionare Nessuno per impedire la conversione delle immagini RGB.

**CMYK:** Definisce lo spazio colore di tutte le immagini CMYK nei file. L&#39;impostazione predefinita è SWOP (U.S. Web Coated) v2. È inoltre possibile selezionare Nessuno per impedire la conversione delle immagini CMYK.

>[!NOTE]
>
>Se si seleziona Nessuno per tutte e tre le aree di lavoro, si ottiene lo stesso effetto della selezione di Lascia colore invariato.

**Mantenere I Valori CMYK Per Gli Spazi Colore CMYK Tarati:** Se questa opzione è selezionata, i valori CMYK indipendenti dalla periferica vengono trattati come valori dipendenti dalla periferica (DeviceCMYK), gli spazi colore indipendenti dalla periferica vengono eliminati e i file PDF/X-1a utilizzano il valore Converti tutti i colori in CMYK. Se deselezionata, gli spazi colore indipendenti dalla periferica vengono convertiti in CMYK se il criterio di gestione del colore è impostato su Converti tutti i colori in CMYK.

### Dati dipendenti dal dispositivo {#device-dependent-data}

Queste opzioni si applicano se si utilizzano documenti creati con applicazioni grafiche e di documentazione di fascia alta, come Adobe Illustrator e Adobe InDesign. Per ulteriori informazioni, consulta la documentazione allegata all’applicazione.

Le funzioni di trasferimento vengono utilizzate per creare effetti artistici e per adattarsi alle specifiche di uno specifico dispositivo di output. Ad esempio, un file destinato all&#39;output su una particolare fotounità può contenere funzioni di trasferimento che compensano il guadagno del punto intrinseco alla stampante.

**Mantieni In Rimozione Colore E Generazione Nero:** Mantiene queste impostazioni se sono presenti nel file PostScript. La generazione del nero calcola la quantità di nero da utilizzare quando si tenta di riprodurre un colore particolare. La rimozione del sottocromo (UCR) riduce la quantità di componenti ciano, magenta e giallo per compensare la quantità di nero aggiunta dalla generazione del nero. Poiché utilizza meno inchiostro, l&#39;UCR è generalmente utilizzato per la carta da giornale e per le scorte non rivestite.

**Quando Vengono Trovate Funzioni Di Trasferimento:** Determina cosa fare quando vengono trovate funzioni di trasferimento:

**Mantieni:** Conserva le funzioni di trasferimento tradizionalmente utilizzate per compensare l&#39;aumento o la perdita di punti che possono verificarsi quando un&#39;immagine viene trasferita sulla pellicola. L&#39;aumento di punti si verifica quando i punti di inchiostro che compongono un&#39;immagine stampata sono più grandi (ad esempio, a causa della diffusione su carta) rispetto allo schermo mezzitoni; la perdita di punti si verifica quando i punti stampano di dimensioni più piccole. Con questa opzione, le funzioni di trasferimento vengono mantenute come parte del file e vengono applicate al file quando viene generato il file.

**Applica:** Non mantiene la funzione di trasferimento, ma la applica al file, che cambia i colori nel file. Questa opzione è utile per creare effetti colore in un file. Per impostazione predefinita, questa opzione è selezionata per le nuove impostazioni.

**Rimuovi:** Rimuove eventuali funzioni di trasferimento applicate. Rimuovere le funzioni di trasferimento applicate a meno che il file PDF non venga inviato allo stesso dispositivo per il quale è stato creato il file PostScript di origine.

**Mantieni informazioni mezzetinte:** Conserva tutte le informazioni sui mezzitoni nei file. Le informazioni sulle mezzetinte sono costituite da punti che controllano la quantità di inchiostro che i dispositivi a mezzetinte si depositano in una posizione specifica sulla carta. Variando la dimensione e la densità dei punti si crea l&#39;illusione di variazioni di colore grigio o continuo. Per un&#39;immagine CMYK vengono utilizzati quattro retini mezzetinte, uno per ogni inchiostro utilizzato nel processo di stampa.

Nella produzione di stampa tradizionale, un mezzitono viene prodotto posizionando uno schermo mezzitoni tra un pezzo di pellicola e l&#39;immagine, e quindi esponendo la pellicola. Gli equivalenti elettronici, come in Adobe Photoshop, consentono agli utenti di specificare gli attributi del retino mezzetinte prima di produrre la pellicola o l&#39;output cartaceo. Le informazioni sui mezzitoni sono destinate all&#39;uso con un particolare dispositivo di output.

## Opzioni avanzate {#advanced-options}

Le opzioni avanzate specificano quali commenti DSC (Document Structuring Conventions) conservare nel file PDF e come impostare altre opzioni che influiscono sulla conversione da PostScript. In un file PostScript, i commenti DSC contengono informazioni sul file, ad esempio l&#39;applicazione di origine, la data di creazione e l&#39;orientamento della pagina. Forniscono inoltre una struttura per le descrizioni delle pagine nel file (ad esempio istruzioni iniziali e finali per una sezione prologo). I commenti DSC possono essere utili quando si stampa o si preme il documento. Per istruzioni sull&#39;accesso alle opzioni avanzate, vedere [Aggiungi o modifica impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Quando si lavora con le opzioni avanzate, è utile avere una conoscenza del linguaggio PostScript e di come viene tradotto in PDF. (vedere [ADOBE POSTSCRIPT 3](https://www.adobe.com/products/postscript/main.html).)

**Consenti al file PostScript di ignorare le impostazioni di Adobe PDF:** Utilizza le impostazioni memorizzate in un file PostScript anziché nel file di impostazioni Adobe PDF corrente. Prima di elaborare un file PostScript, è possibile inserire parametri nel file per controllare i seguenti aspetti:

* compressione di testo e grafica
* downsampling e codifica delle immagini campionate
* incorporamento di tipi di carattere Type 1 e istanze di tipi di carattere Master multipli Type 1

**Consenti oggetti XOb PostScript:** Gli oggetti XOb PostScript memorizzano informazioni che vengono visualizzate in molte pagine dello stesso file, ad esempio un&#39;immagine di sfondo o informazioni su intestazione e piè di pagina. L&#39;utilizzo di oggetti XObject PostScript può rendere più veloce la stampa, ma richiede una maggiore quantità di memoria della stampante. Per impedire la creazione di oggetti XOb PostScript, deselezionate questa opzione se create file PDF con compatibilità Acrobat 5 (PDF 1.4) o successiva.

**Converti sfumature in tonalità smussate:** Converte i raccordi in tonalità uniformi per Acrobat 4 e versioni successive, riducendo le dimensioni dei file PDF e migliorando potenzialmente la qualità dell&#39;output finale. PDF Generator converte le sfumature da Adobe Illustrator, Adobe InDesign, Adobe FreeHand MX, CorelDraw, Quark Xpress e Microsoft PowerPoint.

**Converti linee arrotondate in curve:** Riduce la quantità di punti di controllo utilizzati per creare curve nei disegni CAD, consentendo di ottenere PDF più piccoli e un rendering sullo schermo più veloce.

**Mantieni semantica copia di livello 2:** Utilizza l&#39;operatore copypage definito in PostScript LanguageLevel 2 anziché in PostScript LanguageLevel 3. Se disponi di un file PostScript e selezioni questa opzione, la pagina viene copiata da un operatore copypage. Se questa opzione non è selezionata, viene eseguito l&#39;equivalente di un&#39;operazione showpage, ma lo stato della grafica non viene reinizializzato.

**Mantieni impostazioni sovrastampa:** Mantiene le impostazioni di sovrastampa nei file convertiti in PDF. I colori sovrastampati sono due o più inchiostri stampati uno sopra l&#39;altro. Ad esempio, quando un inchiostro ciano viene stampato su un inchiostro giallo, la sovrastampa risultante è di colore verde. Senza sovrastampa, il giallo sottostante non verrebbe stampato, dando luogo a un colore ciano.

**Sovrastampa Il Valore Predefinito È Diverso Da Zero:** Impedisce agli oggetti sovrastampati con valori CMYK pari a zero di eliminare gli oggetti CMYK sottostanti. Questo effetto viene ottenuto inserendo il parametro dello stato grafico OPM 1 nel file PDF in qualsiasi posizione sia presente l&#39;operatore Setoverprint.

**Salva impostazioni Adobe PDF nel file PDF:** Incorpora il file delle impostazioni utilizzato per creare il file PDF. È possibile aprire e visualizzare il file delle impostazioni (con estensione joboptions) nella finestra di dialogo File allegati di Acrobat. Il file delle impostazioni di Adobe PDF diventa un elemento della struttura EmbeddedFiles all’interno del file PDF.

**Se Possibile, Salva Le Immagini Originali Di JPEG In PDF:** Elabora le immagini JPEG compresse (già compresse con la codifica DCT) senza ricomprimerle. Se questa opzione è selezionata, PDF Generator decomprime le immagini JPEG per assicurarsi che non siano danneggiate. Tuttavia, non ricomprime le immagini valide, quindi elabora l’immagine originale senza toccarla. Se questa opzione è selezionata, le prestazioni migliorano perché si verifica solo la decompressione (non la ricompressione) e i dati immagine e i metadati vengono conservati.

**Salva Job Ticket portatile nel file PDF:** Mantiene un ticket di processo PostScript in un file PDF. Il job ticket contiene informazioni sul file PostScript, ad esempio le dimensioni della pagina, la risoluzione e le informazioni di registrazione dei colori, anziché informazioni sul contenuto. Queste informazioni possono essere utilizzate successivamente in un flusso di lavoro o per la stampa del PDF.

**Utilizzare Prolog.ps ed Epilog.ps:** Invia un prologo e un file epilog con ogni processo. Questi file hanno molti scopi. Ad esempio, è possibile modificare i file di profilo per specificare i frontespizi. È possibile modificare i file Epilog per risolvere una serie di procedure in un file PostScript. Puoi caricare o scaricare i file. Consultate Caricamento e download di file prolog ed epilog.

**Elabora commenti DSC:** Gestisce le informazioni DSC da un file PostScript. Sono disponibili le seguenti opzioni secondarie:

**Registra avvisi DSC:** Visualizza messaggi di avviso sui commenti DSC problematici durante l&#39;elaborazione e li aggiunge a un file di log.

**Mantieni informazioni EPS da DSC:** Conserva le informazioni, ad esempio l’applicazione di origine e la data di creazione di un file EPS. Se questa opzione è deselezionata, la pagina viene ridimensionata e centrata in base all&#39;angolo superiore sinistro dell&#39;oggetto superiore sinistro e all&#39;angolo inferiore destro dell&#39;oggetto inferiore destro della pagina.

**Mantieni commenti OPI:** Conserva le informazioni necessarie per sostituire un&#39;immagine o un commento For Placement Only (FPO) con l&#39;immagine ad alta risoluzione sui server che supportano le versioni 1.3 e 2.0 dell&#39;Open Prepress Interface (OPI).

**Mantieni informazioni documento da DSC:** Conserva informazioni quali titolo, data e ora di creazione. Quando si apre un file di PDF in Acrobat, queste informazioni vengono visualizzate nel pannello Descrizione delle proprietà del documento.

**Ridimensiona immagine di pagina e centro per i file EPS:** Centra un&#39;immagine EPS e ridimensiona la pagina per adattarla perfettamente all&#39;immagine. Questa opzione è valida solo per i processi costituiti da un singolo file EPS.

## Report standard e opzioni di conformità {#standards-reporting-and-compliance-options}

PDF Generator può controllare il contenuto di un documento in un file PostScript per assicurarsi che soddisfi i criteri standard PDF/X-1a, PDF/X-3 o PDF/A prima di creare il file PDF. Per i file compatibili con PDF/X, è inoltre possibile richiedere che il file PostScript soddisfi criteri aggiuntivi selezionando altre opzioni in &quot;Report standard e conformità&quot;. La disponibilità delle opzioni dipende dallo standard selezionato.

I file compatibili con PDF/X vengono utilizzati principalmente come formato standardizzato per lo scambio di file PDF destinati alla produzione di stampe ad alta risoluzione. Se non si sta creando un documento PDF per la produzione di stampe, è possibile ignorare gli standard di conformità PDF/X.

I file compatibili con PDF/A vengono utilizzati principalmente per l’archiviazione. Poiché l&#39;obiettivo è la conservazione a lungo termine, il documento deve contenere solo ciò che è necessario per l&#39;apertura e la visualizzazione per tutta la durata prevista del documento. Ad esempio, i file compatibili con PDF/A possono contenere solo testo, immagini raster e oggetti vettoriali, ma non la crittografia e gli script. Inoltre, tutti i font devono essere incorporati in modo che i documenti possano essere aperti e visualizzati come creati. In altre parole, i documenti conformi a PDF/A sono *più sottile* rispetto ai loro omologhi PDF/X, destinati alla produzione di alta qualità.

>[!NOTE]
>
>Se imposti una cartella controllata per la creazione di file conformi a PDF/A, accertati di non aggiungere protezione alla cartella; lo standard PDF/A non consente la crittografia.

Per istruzioni sull&#39;accesso alle opzioni di reporting e conformità degli Standard, vedi [Aggiungi o modifica impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

**Standard di conformità:** Selezionare uno standard per produrre un report che indichi se il file è conforme ai requisiti e, in caso contrario, quali problemi sono stati riscontrati. Quando Compatibilità nella pagina Impostazioni generali è impostato su Acrobat 4.0, vengono attivate le seguenti opzioni. Quando Compatibilità è impostato su Acrobat 5.0, sono disponibili solo le opzioni Acrobat 5.0 per selezionare. Quando Compatibilità è impostata su un&#39;opzione alternativa, le seguenti opzioni sono disattivate:

* PDF/X-1a (compatibile con Acrobat 4.0)
* PDF/X-3 (compatibile con Acrobat 4.0)
* PDF/X-1a (compatibile con Acrobat 5.0)
* PDF/X-3 (compatibile con Acrobat 5.0)
* PDF/A-1b (compatibile con Acrobat 5.0)

### Opzioni per gli standard PDF/X {#options-for-pdf-x-standards}

**Se non conforme:** Specifica se creare il file PDF se il file PostScript non è conforme ai requisiti PDF/X. Questa opzione è disponibile quando Standard di conformità nella pagina Report standard e conformità è impostato su un&#39;opzione diversa da Nessuno.

**Continua:** Crea un file PDF.

**Annulla processo:** Crea un file PDF solo se il file PostScript soddisfa i requisiti PDF/X delle opzioni di report selezionate ed è altrimenti valido. Se sono selezionate entrambe le opzioni di report PDF/X e il file PostScript soddisfa un solo set di criteri PDF/X (ad esempio, PDF/X-3), PDF Generator crea il file conforme.

**Se Non Sono Specificati Né TrimBox Né ArtBox:** Disponibile quando Standard di conformità nella pagina Report standard e conformità è impostato su un&#39;opzione diversa da Nessuno.

**Segnala come errore:** Contrassegna il file PostScript come non conforme se una delle opzioni di reporting è selezionata e una casella di ritaglio o una casella grafica non è presente in alcuna pagina.

**Imposta TrimBox su MediaBox con offset:** Calcola i valori in punti per la casella di ritaglio in base agli offset per la casella multimediale delle rispettive pagine se non sono specificate né la casella di ritaglio né la casella grafica. La finestra di ritaglio è sempre piccola o più piccola della finestra di supporto che la contiene.

**Se BleedBox Non È Specificato:** Disponibile quando Standard di conformità nella pagina Report standard e conformità è impostato su un&#39;opzione diversa da Nessuno.

**Imposta BleedBox su MediaBox:** Utilizza i valori della media box per la bleed box se questa non è specificata.

**Impostate BleedBox su TrimBox con offset:** Calcola i valori in punti per la casella di pagina al vivo in base agli offset per la casella di rifilo delle rispettive pagine se la casella di pagina al vivo non è specificata. Il rettangolo di selezione è sempre di dimensioni pari o superiori a quelle del rettangolo di selezione.

**Valori Predefiniti Se Non Specificati Nel Documento:** Questa opzione è disponibile quando Standard di conformità nella pagina Report standard e conformità è impostato su un&#39;opzione diversa da Nessuno.

**Nome profilo intento di output:** Indica la condizione di stampa caratterizzata per cui il documento è preparato. Se un documento non specifica un nome OutputIntent, PDF Generator utilizza il valore selezionato da questo menu. È possibile selezionare uno dei nomi specificati oppure immettere un nome nello spazio fornito. Se il flusso di lavoro richiede che il documento specifichi l&#39;intento di output, selezionare Nessuno. Qualsiasi documento che non soddisfa il requisito non supera il controllo di conformità.

**Identificatore condizione di output:** Indica il nome di riferimento specificato dal Registro di sistema del nome del profilo dell&#39;intento di output.

**Condizione di output:** Descrive la condizione di stampa prevista. Questa voce può essere utile per il destinatario previsto del documento PDF.

**Nome registro (URL):** Indica l&#39;indirizzo Web per ulteriori informazioni sul registro. L&#39;URL viene immesso automaticamente per i nomi di registro ICC.

**Intrappolato:** Indica lo stato della registrazione dei colori nel documento. La conformità PDF/X richiede un valore True o False. Se il documento non specifica lo stato di registrazione dei colori, viene utilizzato il valore fornito in questo campo. Se il flusso di lavoro richiede che il documento specifichi lo stato di registrazione dei colori, selezionare Lascia indefinito. Qualsiasi documento che non soddisfa il requisito non supera il controllo di conformità.

### Opzioni per lo standard PDF/A {#options-for-pdf-a-standard}

Queste opzioni sono abilitate quando Compatibilità (nell’area Generale) è impostato su Acrobat 4 (PDF 1.3) o Acrobat 5 (PDF 1.4).

**Se non conforme:** Specifica se creare il file PDF se il file PostScript non è conforme ai requisiti PDF/A.

**Continua:** Crea un file PDF anche se il file PostScript non soddisfa i requisiti dello standard.

**Annulla processo:** Crea un file PDF solo se il file PostScript soddisfa i requisiti PDF/A ed è altrimenti valido.

**Nome profilo intento di output:** Indica la condizione di stampa caratterizzata per la quale il documento è stato preparato ed è richiesta per la conformità PDF/A. Se il flusso di lavoro richiede che il documento specifichi le informazioni sull&#39;intento di output, selezionare &quot;Nessuno&quot;. Il documento non supererà la verifica di conformità se queste informazioni non vengono fornite.

**Condizione di output:** Descrive la condizione di stampa prevista. Questa voce non è obbligatoria, ma può essere utilizzata per fornire informazioni utili al destinatario previsto del documento PDF.

## Opzioni di visualizzazione iniziale {#initial-view-options}

Queste opzioni sono organizzate in tre aree: Opzioni documento, Opzioni finestra e Opzioni interfaccia utente. Per istruzioni sull&#39;accesso alle opzioni della visualizzazione iniziale, vedere [Aggiungi o modifica impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Per utilizzare qualsiasi opzione, selezionate Imposta impostazioni vista iniziale (Set Initial View Settings).

### Opzioni documento {#document-options}

Le opzioni del documento controllano l&#39;aspetto del documento all&#39;interno della finestra del documento, ad esempio il livello di ingrandimento e il modo in cui scorre.

**Mostra:** Determina i riquadri e le schede visualizzati nella finestra dell&#39;applicazione per impostazione predefinita. Pannello Segnalibri e pagina apre il riquadro del documento e visualizza la scheda Segnalibri.

**Layout pagina:** Determina se il documento viene visualizzato in modalità pagina singola, pagina affiancata, pagina continua o pagina affiancata continua.

**Ingrandimento:** Imposta il livello di zoom utilizzato per visualizzare il documento all&#39;apertura. Il valore predefinito utilizza il valore di ingrandimento configurato dall’utente nelle preferenze di Acrobat o Adobe Reader.

**Apri a numero pagina:** Imposta la pagina di apertura del documento, in genere la pagina 1.

>[!NOTE]
>
>L&#39;impostazione predefinita per le opzioni di ingrandimento e layout di pagina utilizza le impostazioni per i singoli utenti nelle preferenze Visualizzazione pagina in Acrobat o Adobe Reader.

### Opzioni finestra {#window-options}

Le opzioni della finestra determinano il modo in cui la finestra si regola nell&#39;area dello schermo quando un utente apre il documento. Tuttavia, le opzioni non hanno alcun effetto quando un documento di PDF viene visualizzato all’interno di un browser web.

**Ridimensiona finestra alla pagina iniziale:** Consente di regolare la finestra del documento in modo che si adatti perfettamente alla pagina di apertura, in base alle opzioni selezionate in Opzioni documento.

**Centro finestra su schermo:** Posiziona la finestra al centro dell&#39;area dello schermo.

**Apri In Modalità A Schermo Intero:** Ingrandisce la finestra del documento e visualizza il documento senza la barra dei menu, la barra degli strumenti o i controlli della finestra.

**Mostra:** Nome file mostra il nome del file nella barra del titolo della finestra. Titolo documento mostra il titolo del documento nella barra del titolo della finestra.

### Opzioni dell’interfaccia utente {#user-interface-options}

Le opzioni dell&#39;interfaccia utente determinano quali controlli vengono visualizzati o nascosti all&#39;apertura del documento.

**Nascondi barra dei menu:** Se selezionata, nasconde la barra dei menu

**Nascondi barre degli strumenti:** Se selezionata, nasconde le barre degli strumenti

**Nascondi controlli finestra:** Se selezionata, nasconde i controlli della finestra

>[!NOTE]
>
>Se si nascondono la barra dei menu e la barra degli strumenti, gli utenti non possono applicare comandi e selezionare strumenti a meno che non conoscano le scelte rapide da tastiera quando aprono il file in Acrobat.

## Caricamento e download di file prolog ed epilog {#uploading-and-downloading-prologue-and-epilogue-files}

I file di profilo vengono utilizzati per aggiungere codice PostScript personalizzato che viene eseguito all&#39;inizio di ogni processo PostScript distillato. I file Epilog vengono utilizzati per aggiungere codice PostScript personalizzato che viene eseguito alla fine di ogni processo PostScript. Puoi scaricare i file prolog ed epilog dal server per salvarli localmente. È possibile scaricare i file per configurarli in modo indipendente o per caricarli in un&#39;altra posizione o in un altro computer.

Questi file hanno molti scopi. Ad esempio, i file prolog possono essere modificati per specificare le copertine; i file epilog possono essere modificati per risolvere una serie di procedure in un file PostScript. Puoi anche selezionare e caricare i file prolog ed epilog da inviare con ciascun processo.

### Scaricare un file prolog o epilogue {#download-a-prologue-or-epilogue-file}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Impostazioni Adobe PDF.
1. Fai clic su Nuovo o sul nome di un’impostazione.
1. Fai clic su Avanzate, quindi, accanto all’opzione Usa Prolog.ps ed Epilog.ps, fai clic su Scarica.
1. Nella pagina Scarica prologo ed Epilog file, fai clic su Prolog.ps o Epilog.ps e poi su Salva.

### Caricare un file prolog o epilog {#upload-a-prologue-or-epilogue-file}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > Impostazioni Adobe PDF.
1. Fai clic su Nuovo o sul nome di un’impostazione.
1. Fai clic su Avanzate, quindi, accanto all’opzione Usa Prolog.ps ed Epilog.ps, fai clic su Carica.
1. Nella pagina Carica prologo e file di epilogazione fare clic su Sfoglia per selezionare un prologo o un file di epilogo.
1. Individuare il file e fare clic su Apri.
1. Per utilizzare il file, accertati che l’opzione Usa Prolog.ps ed Epilog.ps sia selezionata nell’area Avanzate della pagina Nuova/Modifica impostazione di Adobe PDF.
1. Fai clic su Salva

>[!NOTE]
>
>PDF Generator supporta i file prolog ed epilog solo per la conversione di file PostScript e PostScript incapsulati in PDF.
