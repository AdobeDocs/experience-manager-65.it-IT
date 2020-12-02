---
title: Configurazione  impostazioni Adobe PDF
seo-title: Configurazione  impostazioni Adobe PDF
description: Scoprite come configurare  impostazioni Adobe PDF.
seo-description: Scoprite come configurare  impostazioni Adobe PDF.
uuid: 980c9d6a-f75e-4e7d-b050-d2d07a10ef33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab018b6d-0233-4439-bb75-58c5421d769a
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '7276'
ht-degree: 0%

---


# Configurazione  impostazioni Adobe PDF{#configuring-adobe-pdf-settings}

Nella pagina  Impostazioni Adobe PDF sono visualizzate le impostazioni di conversione che potete specificare per le sorgenti da utilizzare. È possibile utilizzare una qualsiasi delle impostazioni PDF predefinite o crearne una personalizzata. Le impostazioni PDF determinano con precisione la modalità di conversione dei file e la struttura e le funzioni PDF che ne risultano.  impostazioni Adobe PDF erano precedentemente note come parametri Distiller® o opzioni di processo.

Nella  pagina Impostazioni Adobe PDF potete effettuare le seguenti operazioni:

* Visualizzare le impostazioni PDF predefinite. (Vedere [Informazioni sulle impostazioni PDF predefinite](configuring-pdf-settings.md#about-the-predefined-pdf-settings).)
* Creare un’impostazione PDF o modificarne una creata in precedenza. (Vedere [Aggiungere o modificare le impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).)
* Specificare le impostazioni PDF predefinite. (Vedere [Modifica delle impostazioni predefinite](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings))
* Caricate un file di impostazioni PDF sul server. (Vedere [Carica impostazioni PDF](configuring-pdf-settings.md#upload-pdf-settings).)
* Eliminare le impostazioni PDF personalizzate. (Vedere [Elimina impostazioni PDF](configuring-pdf-settings.md#delete-pdf-settings).)
* Caricate e scaricate i file prolog ed epilog. (Vedere [Caricamento e download di file prolog ed epilog](configuring-pdf-settings.md#uploading-and-downloading-prologue-and-epilogue-files).)

 impostazioni Adobe PDF sono applicabili solo alle conversioni basate su PDFMaker. Queste includono le seguenti conversioni:

* Documento di Microsoft Word (DOC, DOCX, RTF, TXT)
* Documento Microsoft Excel (XLS, XLSX)
* Documento di Microsoft PowerPoint (PPT, PPTX)
* Documento di progetto Microsoft (MPP)
* Documento di Microsoft Visio (VSD)

>[!NOTE]
>
>Quando si utilizza OpenOffice per convertire i formati indicati sopra,  impostazioni Adobe PDF non vengono applicate.

## Informazioni sulle impostazioni PDF predefinite {#about-the-predefined-pdf-settings}

PDF Generator offre diverse impostazioni PDF predefinite. Non è possibile modificare tali impostazioni predefinite; tuttavia, potete creare un’impostazione basata su una esistente modificando l’impostazione e salvandola con un nuovo nome.

**Stampa di alta qualità:** crea file PDF per un output di alta qualità. Questa impostazione:

* downsampling a 300 dpi delle immagini a colori e in scala di grigi
* downsampling immagini monocromatiche a 1200 dpi
* stampa a una risoluzione immagine più elevata
* utilizza altre impostazioni per mantenere la quantità massima di informazioni sul documento originale.

Questi file PDF possono essere aperti in  Adobe Acrobat 5 e  Adobe Acrobat Reader® 5 o versione successiva.

**Pagine oversize:** Crea documenti PDF adatti per la visualizzazione e la stampa affidabili di disegni tecnici di dimensioni superiori a 200 x 200 pollici. I documenti PDF creati possono essere aperti in  Adobe Acrobat Professional e  Acrobat Standard, versione 7 o successiva e  Adobe Reader 7 o versione successiva.

**PDF/A-1B 2005 CMYK / PDF/A-1B 2005 RGB:** verifica i processi in entrata per la conformità allo standard ISO per la conservazione a lungo termine (archiviazione) dei documenti elettronici e crea file PDF/A solo se conformi. Questi file vengono utilizzati principalmente per l&#39;archiviazione. I file conformi possono contenere solo testo, immagini raster e oggetti vettoriali; non possono contenere cifratura e script. Inoltre, tutti i font devono essere incorporati in modo che i documenti possano essere aperti e visualizzati come creati. PDF/A-1b utilizza PDF 1.4 e converte tutti i colori in CMYK o RGB, a seconda dello standard scelto. I file PDF creati con questo file di impostazioni possono essere aperti in  Acrobat 5 e  Acrobat Reader 5 e versioni successive. Per ulteriori informazioni sui PDF/A, vedere  standard di Adobe e di settore.

**PDF/X-1a 2001:** verifica la conformità ai processi in entrata per PDF/X-1a e crea file PDF solo se conformi. PDF/X-1a è uno standard ISO per lo scambio di contenuti grafici. PDF/X-1a richiede l&#39;incorporazione di tutti i font, la specificazione delle caselle PDF appropriate e la visualizzazione del colore come CMYK o tinte piatte. I file PDF che soddisfano i requisiti PDF/X-1a sono destinati a una condizione di output specifica, ad esempio la stampa offset Web in base alle specifiche Pubblicazioni offset Web. Per ulteriori informazioni sui PDF/X, vedere  standard di Adobe e di settore.

**PDF/X-3 2002:** verifica i processi in entrata per la conformità PDF/X-3 e crea file PDF solo se conformi. Come PDF/X-1a, PDF/X-3 è uno standard ISO per lo scambio di contenuti grafici. La differenza principale è che PDF/X-3 supporta il colore indipendente dalla periferica.

**Qualità stampa:** crea file PDF per la produzione di stampe di alta qualità (ad esempio, su una fotounità o una piastrina). In questo caso, la dimensione del file non è una considerazione. L&#39;obiettivo è mantenere tutte le informazioni contenute in un file PDF che una stampante commerciale o un fornitore di servizi di prestampa deve stampare correttamente. Questo insieme di opzioni:

* downsampling a 300 dpi delle immagini a colori e in scala di grigi
* downsampling immagini monocromatiche a 1200 dpi
* incorpora sottoinsiemi di tutti i font utilizzati nel documento
* stampa a una risoluzione immagine più elevata,
* non ruota automaticamente le pagine in base all&#39;orientamento dei commenti DSC (Text Format Convention) o delle convenzioni di strutturazione del testo
* utilizza altre impostazioni per mantenere la quantità massima di informazioni sul documento originale.

I processi di stampa non riescono in presenza di font che non possono essere incorporati. Questi file PDF possono essere aperti in  Acrobat 5 e  Acrobat Reader 5 e versioni successive.

>[!NOTE]
>
>Prima di creare un file PDF da inviare a una stampante commerciale o a un fornitore di servizi di prestampa, determinare la risoluzione di output e altre impostazioni oppure richiedere un file .joboptions con le impostazioni consigliate. Potrebbe essere necessario personalizzare le impostazioni Adobe PDF  per un particolare fornitore e fornire un file .joboptions personalizzato.

**Dimensioni file più ridotte:** crea file PDF per la visualizzazione sul Web o su una Intranet o per la distribuzione tramite un sistema e-mail per la visualizzazione a schermo. Questa serie di opzioni utilizza la compressione, il downsampling e una risoluzione delle immagini relativamente bassa. Converte tutti i colori in sRGB e non incorpora i font a meno che non sia necessario. Ottimizza anche i file per la trasmissione dei byte. Questi file PDF possono essere aperti in  Acrobat 5 e  Acrobat Reader 5.0 e versioni successive.

**Standard:** consente di creare file PDF da stampare su stampanti desktop o fotocopiatrici digitali, da pubblicare su CD o da inviare a un client come prova di pubblicazione. Questo set di opzioni utilizza la compressione e il downsampling per ridurre la dimensione del file. Incorpora inoltre sottoinsiemi di tutti i font utilizzati nel file, converte tutti i colori in sRGB e stampa a una risoluzione media per creare una rappresentazione ragionevolmente accurata del documento originale. I sottoinsiemi di font di Microsoft Windows non sono incorporati per impostazione predefinita. Questi file PDF possono essere aperti in  Acrobat 5 e  Acrobat Reader 5.0 e versioni successive.

## Aggiungere o modificare le impostazioni PDF {#add-or-edit-pdf-settings}

Le impostazioni PDF determinano con precisione come vengono convertiti i file e la struttura e le funzioni PDF che ne risultano. Definire una nuova impostazione PDF o modificarne una creata in precedenza. Non potete modificare le impostazioni predefinite, ma potete creare un&#39;impostazione basata su una esistente modificando l&#39;impostazione e salvandola con un nuovo nome.

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator >  Impostazioni Adobe PDF.
1. Fate clic su Nuovo oppure fate clic sul nome di un’impostazione esistente.
1. Nella pagina Nuovo/Modifica  Impostazione Adobe PDF, completa le informazioni richieste nelle seguenti sezioni:

   [Opzioni generali](configuring-pdf-settings.md#general-options)

   [Opzioni Immagini](configuring-pdf-settings.md#images-options)

   [Opzioni dei font](configuring-pdf-settings.md#fonts-options)

   [Opzioni colore](configuring-pdf-settings.md#color-options)

   [Opzioni avanzate](configuring-pdf-settings.md#advanced-options)

   [Standard, opzioni di reporting e conformità](configuring-pdf-settings.md#standards-reporting-and-compliance-options)

   [Opzioni di visualizzazione iniziali](configuring-pdf-settings.md#initial-view-options)

   Per passare a un’altra sezione, fate clic sul relativo collegamento nella pagina Web o utilizzate i pulsanti Successivo e Precedente.

1. Dopo aver completato le informazioni in tutte le sezioni, fate clic su Salva o Salva con nome e specificate un nome per l’impostazione.

## Carica impostazioni PDF {#upload-pdf-settings}

È possibile disporre delle impostazioni PDF sul server PDF Generator caricandole da un computer locale o da un percorso di rete.

1. Nella console di amministrazione, fate clic su Servizi > PDF Generator >  impostazioni Adobe PDF e fate clic su Carica.
1. Nella pagina Carica  Impostazioni Adobe PDF, fate clic su Sfoglia, individuate il file delle impostazioni PDF e fate clic su Apri.
1. Fate clic su OK, quindi di nuovo su OK.

## Elimina impostazioni PDF {#delete-pdf-settings}

Se non sono più necessarie, è possibile eliminare definitivamente le impostazioni PDF.

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator >  Impostazioni Adobe PDF.
1. Selezionate la casella accanto all’impostazione da eliminare. Potete selezionare più impostazioni.
1. Fate clic su Elimina e, nella pagina Elimina conferma, fate di nuovo clic su Elimina.

## Opzioni generali {#general-options}

Utilizzate le opzioni generali per specificare la versione di  Acrobat da utilizzare per la compatibilità dei file e altre opzioni di file e dispositivi. Per istruzioni su come accedere alle opzioni Generali, vedere [Aggiungere o modificare le impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Opzioni file {#file-options}

**Compatibilità:** il livello di compatibilità del file PDF. Per i documenti che verranno distribuiti su larga scala, è consigliabile selezionare  Acrobat 4 (PDF 1.3) o  Acrobat 5 (PDF 1.4) per garantire che tutti gli utenti possano visualizzare e stampare il documento. Se create dei file utilizzando  compatibilità Acrobat 5 o versioni successive, questi potrebbero non essere compatibili con le versioni precedenti di  Acrobat. Le sottosezioni seguenti mostrano alcune delle differenze tra i file PDF creati utilizzando diversi livelli di compatibilità  Acrobat.

<table>
 <tbody>
  <tr>
   <th><p> Acrobat 4 (PDF 1.3)</p> </th>
   <th><p> Acrobat 5 (PDF 1.4)</p> </th>
   <th><p> Acrobat 6 (PDF 1.5)</p> </th>
   <th><p> Acrobat 7 (PDF 1.6) e  Acrobat 8 (PDF 1.7)</p> </th>
  </tr>
  <tr>
   <td><p>Può essere aperto con  Acrobat 3.0 e  Acrobat Reader 3.0 e versioni successive.</p> </td>
   <td><p>Può essere aperto con  Acrobat 3.0 e  Acrobat Reader 3.0 e versioni successive. Le funzioni specifiche delle versioni successive potrebbero essere perse o non essere visualizzate.</p> </td>
   <td><p>La maggior parte può essere aperta con  Acrobat 4 e  Acrobat Reader 4.0 e versioni successive. Le funzioni specifiche delle versioni successive potrebbero essere perse o non essere visualizzate.</p> </td>
   <td><p>La maggior parte può essere aperta con  Acrobat 4 e  Acrobat Reader 4.0 e versioni successive. Le funzioni specifiche delle versioni successive potrebbero essere perse o non essere visualizzate.</p> </td>
  </tr>
  <tr>
   <td><p>Non può contenere immagini che utilizzano effetti di trasparenza dinamici. Qualsiasi trasparenza deve essere appiattita prima di convertirla in PDF 1.3.</p> </td>
   <td><p>Supporta l'utilizzo della trasparenza dal vivo nelle immagini.  funzione Acrobat Distiller appiattisce la trasparenza.</p> </td>
   <td><p>Supporta l'utilizzo della trasparenza dal vivo nelle immagini.  funzione Acrobat Distiller appiattisce la trasparenza.</p> </td>
   <td><p>Supporta l'utilizzo della trasparenza dal vivo nelle immagini.  funzione Acrobat Distiller appiattisce la trasparenza.</p> </td>
  </tr>
  <tr>
   <td><p>I livelli non sono supportati.</p> </td>
   <td><p>I livelli non sono supportati.</p> </td>
   <td><p>Mantiene i livelli durante la creazione di file PDF da applicazioni che supportano la generazione di documenti PDF a livelli, come  Adobe Illustrator® CS o  Adobe InDesign® CS e versioni successive.</p> </td>
   <td><p>Mantiene i livelli durante la creazione di file PDF da applicazioni che supportano la generazione di documenti PDF a livelli, come  Illustrator CS o  InDesign CS e versioni successive.</p> </td>
  </tr>
  <tr>
   <td><p>È supportato lo spazio colore DeviceN con 8 coloranti.</p> </td>
   <td><p>È supportato lo spazio colore DeviceN con 8 coloranti.</p> </td>
   <td><p>È supportato lo spazio colore DeviceN con fino a 31 coloranti.</p> </td>
   <td><p>È supportato lo spazio colore DeviceN con fino a 31 coloranti.</p> </td>
  </tr>
  <tr>
   <td><p>I font multibyte possono essere incorporati. (Distiller converte i font durante l’incorporazione.)</p> </td>
   <td><p>I font multibyte possono essere incorporati.</p> </td>
   <td><p>I font multibyte possono essere incorporati.</p> </td>
   <td><p>I font multibyte possono essere incorporati.</p> </td>
  </tr>
  <tr>
   <td><p>È supportata la sicurezza RC4 a 40 bit.</p> </td>
   <td><p>È supportata la sicurezza RC4 a 128 bit.</p> </td>
   <td><p>È supportata la sicurezza RC4 a 128 bit.</p> </td>
   <td><p>È supportata la sicurezza RC4 a 128 bit e AES a 128 bit (Advanced Encryption Standard).</p> </td>
  </tr>
 </tbody>
</table>

**Compressione a livello di oggetto:** Raggruppa oggetti di piccole dimensioni (ciascuno dei quali non è comprimibile) in flussi che possono quindi essere compressi in modo efficiente.

**Disattivato:** non comprime alcuna informazione strutturale nel documento PDF. Selezionate questa opzione se desiderate che gli utenti possano visualizzare, navigare e interagire con segnalibri e altre informazioni strutturali utilizzando  Acrobat 5 e versioni successive.

**Solo tag:** Comprime le informazioni strutturali nel documento PDF. Questa opzione consente di creare un file PDF che può essere aperto e stampato utilizzando  Acrobat 5. Gli utenti non possono visualizzare informazioni su accessibilità, struttura o PDF con tag in  Acrobat 5 o  Acrobat Reader 5.0, ma possono visualizzare tali informazioni  Acrobat 6 e  Adobe Reader 6.0.

**Rotazione automatica pagine:** imposta la rotazione automatica delle pagine in base all&#39;orientamento del testo o dei commenti DSC. Ad esempio, alcune pagine (ad esempio, pagine contenenti tabelle) potrebbero richiedere all&#39;utente di ruotare le pagine lateralmente per leggerle. Selezionate Singolarmente per ruotare ogni pagina in base alla direzione del testo su quella pagina. Per ruotare tutte le pagine del documento in base all’orientamento della maggior parte del testo, selezionate Raccolti per file.

>[!NOTE]
>
>Se Elabora commenti DSC è selezionato nelle impostazioni Avanzate e se sono inclusi i commenti di orientamento %%Viewing, tali commenti hanno precedenza nel determinare l&#39;orientamento della pagina.

**Binding:** specifica se visualizzare un file PDF con binding a sinistra o a destra. Questa impostazione influisce sulla visualizzazione delle pagine nella pagina di fronte - Layout continuo e sulla visualizzazione delle miniature affiancate.

**Risoluzione:** imposta l&#39;emulazione per la risoluzione di una stampante per i file di input che regolano il loro comportamento in base alla risoluzione della stampante su cui vengono stampati. Per la maggior parte dei file di input, un’impostazione di risoluzione più elevata genera file PDF di qualità maggiore ma di qualità superiore e un’impostazione più bassa produce file PDF di qualità inferiore ma di dimensioni più ridotte. Nella maggior parte dei casi, la risoluzione determina il numero di passaggi in una sfumatura o fusione. È possibile immettere un valore compreso tra 72 e 4000. Mantenere questa impostazione come predefinita a meno che non si intenda stampare il file PDF su una stampante specifica e si desideri emulare la risoluzione definita nel file di input originale.

>[!NOTE]
>
>Aumentando l&#39;impostazione della risoluzione, la dimensione del file aumenta e potrebbe aumentare leggermente il tempo necessario per elaborare alcuni file.

**Tutte le pagine o Pagine da:** specifica quali pagine convertire. Lasciate vuota la casella A per creare un intervallo dal numero di pagina immesso nella casella Da alla fine del file.

**Ottimizza per visualizzazione Web veloce:** riorganizza il file per il download di pagine alla volta (trasmissione di byte) dai server Web. Questa opzione comprime testo e grafica, indipendentemente da quanto selezionato come impostazioni di compressione nella scheda Immagini. La compressione consente un accesso e una visualizzazione più veloci durante il download del file dal Web o da una rete. Per impostazione predefinita, questa opzione non è abilitata.

### Dimensioni pagina predefinite {#default-page-size}

Le opzioni Dimensione pagina predefinita specificano le dimensioni di pagina da utilizzare quando non ne viene specificata una nel file originale. In genere,  file Adobe PostScript includono queste informazioni, fatta eccezione per i file Encapsulated PostScript (EPS), che danno una dimensione limite ma non una dimensione di pagina. La dimensione massima consentita per la pagina è di 15.000.000 pollici (31.800.000 cm) in entrambe le direzioni. Queste opzioni configurano le dimensioni predefinite della pagina:

**Larghezza:** Larghezza della pagina

**Altezza:** Altezza della pagina

**Unità:** unità da usare per le impostazioni di larghezza e altezza

## Opzioni immagini {#images-options}

Le opzioni Immagini specificano la compressione e il ricampionamento delle immagini. Potete provare a utilizzare queste opzioni per trovare un equilibrio appropriato tra la dimensione del file e la qualità dell&#39;immagine. Per istruzioni su come accedere alle impostazioni Immagini, vedere [Aggiungere o modificare le impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Queste opzioni configurano immagini a colori, in scala di grigio e monocromatiche:

**Downsampling:** imposta un valore per ciascun tipo di immagine. Per eseguire il downsampling di immagini a colori, in scala di grigi o monocromatiche, PDF Generator combina i pixel in un’area campione per ingrandire un pixel. Specificate la risoluzione del dispositivo di output in punti per pollice (dpi) e immettete una risoluzione in dpi nella casella Per immagini sopra. Per le immagini con una risoluzione superiore a tale soglia, PDF Generator combina i pixel, in base alle esigenze, per ridurre la risoluzione dell’immagine (pixel per pollice) all’impostazione dpi specificata. Per disattivare il downsampling, selezionate Disattivato. Di seguito sono riportate le opzioni disponibili:

**Downsampling medio a:** calcola la media dei pixel in un’area campione e sostituisce l’intera area con il colore medio in pixel alla risoluzione specificata.

**Downsampling bicubico a:** utilizza una media ponderata per determinare il colore dei pixel e in genere produce risultati migliori rispetto al metodo di downsampling della media semplice. Il bicubico è il metodo più lento ma più preciso e produce le gradazioni tonali più omogenee.

**Sottocampionamento A:** seleziona un pixel al centro dell’area di esempio e sostituisce l’intera area con tale pixel alla risoluzione specificata. Il sottocampionamento riduce notevolmente il tempo di conversione rispetto al downsampling, ma produce immagini meno uniformi e continue.

L&#39;impostazione di risoluzione per il colore e la scala di grigi deve essere da 1,5 a 2 volte superiore alla schermata della linea in cui il file verrà stampato. A condizione che non si vada al di sotto di questa impostazione di risoluzione consigliata, le immagini che non contengono linee rette o pattern geometrici o ripetuti non sono interessate da una risoluzione inferiore. La risoluzione per le immagini monocromatiche deve essere la stessa della periferica di output. Tuttavia, tenete presente che il salvataggio di un’immagine monocromatica a una risoluzione superiore a 1500 dpi aumenta le dimensioni del file senza che sia stato migliorato notevolmente la qualità dell’immagine.

È inoltre opportuno considerare se gli utenti devono ingrandire una pagina. Ad esempio, se create un documento PDF di una mappa, provate a usare una risoluzione immagine più elevata in modo che gli utenti possano ingrandire la mappa.

>[!NOTE]
>
>Il ricampionamento delle immagini monocromatiche può produrre risultati di visualizzazione imprevisti, ad esempio nessuna visualizzazione delle immagini. Se si verifica questo problema, disattivate il ricampionamento e convertite di nuovo il file. Questo problema si verifica con maggiore probabilità con il sottocampionamento e con minore probabilità con il downsampling bicubico.

La tabella riportata di seguito contiene i tipi di stampanti e la relativa risoluzione, misurati in dpi, la loro risoluzione predefinita dello schermo misurata in linee per pollice (lpi) e una risoluzione di ricampionamento per le immagini misurate in pixel per pollice (ppi). Ad esempio, per stampare su una stampante laser a 600 dpi, immettere 170 per la risoluzione a cui campionare le immagini.

<table>
 <tbody>
  <tr>
   <th><p>Risoluzione della stampante</p> </th>
   <th><p>Schermata di linea predefinita</p> </th>
   <th><p>Risoluzione delle immagini</p> </th>
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
   <td><p>2400 dpi (imagesetter)</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

**Compressione:** impostate un valore da applicare alle immagini a colori, in scala di grigi e monocromatiche. Per le immagini a colori e in scala di grigio, impostate anche la qualità dell’immagine:

* Per le immagini a colori o in scala di grigi, selezionate ZIP per applicare una compressione che funzioni bene per le immagini con ampie aree di colori singoli o motivi ripetuti. Esempi sono le schermate, semplici immagini create con programmi di pittura e immagini monocromatiche contenenti pattern ripetuti. Selezionate JPEG, qualità minima fino al massimo, per applicare una compressione adatta per le immagini in scala di grigio o a colori, ad esempio fotografie a toni continui che contengono più dettagli di quanti possano essere riprodotte sullo schermo o sulla stampa. Selezionate Automatico (JPEG) per determinare automaticamente la qualità migliore per le immagini a colori e in scala di grigi.
* Per le immagini monocromatiche, selezionate la compressione CCITT Group 4, CCITT Group 3, ZIP, JPEG200, Automatic (JPEG2000) o Run Length.

Accertatevi che le immagini monocromatiche siano digitalizzate come immagini monocromatiche e non come immagini in scala di grigio. Il testo acquisito viene talvolta salvato come immagini in scala di grigio per impostazione predefinita. Il testo in scala di grigio compresso con il metodo di compressione JPEG non è chiaro e potrebbe essere illeggibile.

**Qualità immagine:** configura la qualità dell’immagine per le immagini a colori e in scala di grigi. Le opzioni sono minimo, basso, medio, alto e massimo.

**Antialiasing su grigio:** smussa i bordi delle immagini monocromatiche. Selezionate 2 bit, 4 bit o 8 bit per specificare 4, 16 o 256 livelli di grigio. (l&#39;anti-alias può sfocare righe sottili o di tipo piccolo.)

>[!NOTE]
>
>La compressione di testo e grafica è sempre attiva.

**Criteri immagine:** impostare un criterio per le immagini a colori, in scala di grigi e monocromatiche. Se la risoluzione dell’immagine è inferiore alla risoluzione specificata, potete comunque selezionare di continuare (Ignora), fornire un messaggio di avviso o annullare il processo.

## Opzioni dei font {#fonts-options}

Le opzioni Font specificano i font da incorporare in un file PDF e se incorporare un sottoinsieme di caratteri utilizzati nel file PDF. Per istruzioni su come accedere alle opzioni Font, vedere [Aggiungere o modificare le impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

>[!NOTE]
>
>Quando si combinano file PDF con lo stesso sottoinsieme di font, PDF Generator tenta di combinare i sottoinsiemi di font.

**Incorpora tutti i font:** incorpora tutti i font utilizzati nel file. L&#39;incorporazione dei font è necessaria per la conformità PDF/X.

**Sottoinsieme Font incorporati Quando la percentuale di caratteri utilizzati è minore di:** Se selezionate questa opzione, specificate una percentuale di soglia per incorporare solo un sottoinsieme di font. Ad esempio, se la soglia è 35 e viene utilizzato meno del 35% dei caratteri, PDF Generator incorpora solo tali caratteri. Vengono incorporati solo i font con i bit di autorizzazione appropriati.

**In caso di mancata incorporazione:** specifica come PDF Generator risponde se non riesce a trovare un font da incorporare durante l&#39;elaborazione di un file. È possibile fare in modo che PDF Generator ignori la richiesta e sostituisca il font, avvisi e sostituisca il font oppure annulli l&#39;elaborazione del processo corrente.

**Origine font:** la posizione dei font utilizzati da PDF Generator.

### Specificare i font da incorporare {#specify-which-fonts-to-embed}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator >  Impostazioni Adobe PDF.
1. Fate clic su Nuovo o sul nome di un’impostazione.
1. Fate clic su Font e deselezionate Incorpora tutti i font.
1. Dall&#39;elenco Origine font, selezionare un&#39;origine font e fare clic su Vai per aggiornare l&#39;elenco dei font nella casella a sinistra.
1. Fare clic su un font nella casella a sinistra. Fate clic su Aggiungi accanto alla casella appropriata per spostarla nell’elenco Incorpora sempre o Non incorporare mai. Ripetere la procedura per ciascun font. Tenete premuto Ctrl e fate clic per selezionare più font da spostare.
1. Per rimuovere un font dall&#39;elenco Incorpora sempre o Non incorporare mai, selezionatelo e fate clic su Rimuovi accanto alla casella appropriata. Questa azione non rimuove il font dal sistema; elimina il riferimento nell&#39;elenco.
1. Se il font che si desidera specificare non viene visualizzato, digitarne il nome nella casella Aggiungi font, quindi fare clic su Incorpora sempre o Non incorporare mai. I nomi dei font non possono contenere caratteri alfanumerici.

>[!NOTE]
>
>Un font TrueType può contenere un&#39;impostazione aggiunta dal designer dei font che impedisce l&#39;incorporazione del font nei file PDF.

>[!NOTE]
>
>I font vengono selezionati dalla cache dei font di sistema di Windows e per aggiornare la cache è necessario riavviare il sistema. Dopo aver specificato la directory dei font del cliente, assicurarsi di riavviare il sistema in cui sono installati AEM moduli.

## Opzioni colore {#color-options}

Le opzioni Colore impostano tutte le informazioni sulla gestione del colore per PDF Generator. Per istruzioni su come accedere alle opzioni Colore, vedere [Aggiungere o modificare le impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

###  impostazioni Adobe Color {#adobe-color-settings}

**File impostazioni:** Questo elenco contiene un elenco delle impostazioni colore utilizzate anche nelle principali applicazioni grafiche, come  Adobe Photoshop e  Adobe Illustrator. L’impostazione del colore selezionata determina le altre impostazioni di colore  Adobe nella pagina. Ad esempio, se si seleziona un&#39;impostazione diversa da Nessuno, tutte le opzioni diverse da quelle per Dati dipendenti dal dispositivo sono predefinite e attenuate. È possibile modificare le impostazioni Criteri di gestione colore e Spazi di lavoro solo se si seleziona Nessuno per File impostazioni.

### Criteri di gestione del colore {#color-management-policies}

Se per il file delle impostazioni è stato selezionato Nessuno, l&#39;area Criteri di gestione colore specifica in che modo PDF Generator converte il colore non gestito in un file PostScript.

**Mantieni colore invariato:** lascia invariati i colori dipendenti dalla periferica e mantiene i colori indipendenti dalla periferica come l’equivalente più vicino possibile in PDF. Questa opzione è utile per i laboratori di stampa che hanno calibrato tutti i loro dispositivi, utilizzato quelle informazioni per specificare il colore nel file e l&#39;output solo per tali dispositivi.

**Tag Tutto per Gestione colore:** incorpora un profilo Consorzio colore internazionale quando si distendono i file e si calibrano i colori nelle immagini, il che rende i colori nei file PDF risultanti indipendenti dalla periferica se si seleziona  compatibilità Acrobat 4 (PDF 1.3) o versioni successive. Tuttavia, gli spazi colore dipendenti dalla periferica nei file (RGB, Scala di grigio e CMYK) vengono convertiti in spazi colore indipendenti dalla periferica (CalRGB, CalGray e LAB).

**Tag Only Images for Color Management:** incorpora i profili ICC solo nelle immagini, non nel testo o negli elementi grafici, quando si distribuiscono i file se è stata selezionata  compatibilità con Acrobat 4 (PDF 1.3). Questa opzione impedisce che il testo nero subisca uno spostamento del colore. Tuttavia, gli spazi colore dipendenti dal dispositivo nelle immagini (RGB, Scala di grigio e CMYK) vengono convertiti in spazi colore indipendenti dal dispositivo (CalRGB, CalGray e LAB). Testo e grafica non sono convertiti.

**Converti tutti i colori in sRGB o Converti tutti i colori in CMYK:** Calcola il colore nel file, rendendo il dispositivo di colore indipendente, simile a Tag Tutto per Gestione colore. Se avete selezionato  compatibilità Acrobat 4 (PDF 1.3) o versioni successive e convertite in sRGB, le immagini CMYK e RGB vengono convertite in sRGB.

Indipendentemente dall’opzione di compatibilità selezionata, le immagini in scala di grigio restano invariate. In genere questo riduce le dimensioni e aumenta la velocità di visualizzazione dei file PDF, poiché per descrivere le immagini RGB è necessario disporre di meno informazioni rispetto a quelle per descrivere le immagini CMYK. Poiché RGB è lo spazio colore nativo utilizzato sui monitor, non è necessaria alcuna conversione del colore durante la visualizzazione, il che contribuisce a una rapida visualizzazione online. Questa opzione è consigliata se il file PDF è destinato all’uso online o con stampanti a bassa risoluzione.

**Intento di rendering del documento:** metodo per mappare i colori tra gli spazi colore. Il risultato di un particolare metodo dipende dai profili degli spazi colore. Ad esempio, alcuni profili producono risultati identici con metodi diversi. Le opzioni disponibili sono:

>[!NOTE]
>
>In tutti i casi, gli intenti possono essere ignorati o sostituiti da operazioni di gestione del colore che si verificano dopo la creazione del file PDF.

**Mantieni:** indica che l&#39;intento è specificato nella periferica di output anziché nel file PDF. In molti dispositivi di output, Colorimetria relativa è l&#39;intento predefinito.

**Percettivo:** mantiene i valori di colore relativi tra i pixel originali mentre vengono mappati sulla gamma di destinazione. Questo metodo mantiene la relazione visiva tra i colori, anche se i valori dei colori stessi possono variare.

**Saturazione:** mantiene i valori di saturazione relativi dei pixel originali. Questo metodo è adatto per la grafica aziendale, dove la relazione esatta tra i colori non è importante quanto avere colori saturi brillanti.

**Colorimetrica relativa:** rimette il punto bianco dello spazio sorgente nel punto bianco dello spazio di destinazione.

**Colorimetrica assoluta:** disattiva la corrispondenza dei punti bianchi e neri durante la conversione dei colori. Questo metodo è consigliato solo se è necessario conservare i colori della firma, ad esempio quelli utilizzati in marchi o logo.

### Spazi di lavoro {#working-spaces}

Per tutti i valori nell’elenco Criteri di gestione colore, diversi da Lascia invariato colore, selezionare dagli elenchi nell’area Spazio di lavoro per specificare quali profili ICC vengono utilizzati per definire e calibrare gli spazi colore scala di grigio, RGB e CMYK nei file PDF distillati. Le opzioni disponibili sono:

**Grigio:** definisce lo spazio colore di tutte le immagini in scala di grigio nei file. Questa opzione è disponibile solo se avete scelto Tag Tutto per Gestione colore o Tag Solo Immagini per Gestione colore. Il profilo ICC predefinito per le immagini in grigio è Gamma 2.2. Potete anche selezionare Nessuno per evitare che le immagini in scala di grigio vengano convertite.

**RGB:** definisce lo spazio colore di tutte le immagini RGB nei file. Il valore predefinito, sRGB IEC61966-2.1, è generalmente una buona scelta perché sta diventando uno standard di settore e molti dispositivi di output lo riconoscono. Potete anche selezionare Nessuno per evitare che le immagini RGB vengano convertite.

**CMYK:** definisce lo spazio colore di tutte le immagini CMYK nei file. Il valore predefinito è US Web Coated (SWOP) v2. Potete anche selezionare Nessuno per impedire la conversione delle immagini CMYK.

>[!NOTE]
>
>La selezione di Nessuno per tutti e tre gli spazi di lavoro ha lo stesso effetto della selezione di Mantieni colore invariato.

**Mantieni valori CMYK per gli spazi colore CMYK calibrati:** quando è selezionata questa opzione, i valori CMYK indipendenti dalla periferica vengono trattati come valori dipendenti dalla periferica (DeviceCMYK), gli spazi colore indipendenti dalla periferica vengono scartati e i file PDF/X-1a utilizzano il valore Converti tutti i colori in CMYK. Se questa opzione è deselezionata, gli spazi colore indipendenti dalla periferica vengono convertiti in CMYK se il criterio di gestione del colore è impostato su Converti tutti i colori in CMYK.

### Dati dipendenti dal dispositivo {#device-dependent-data}

Queste opzioni si applicano se lavorate con documenti creati con applicazioni di documentazione e grafica high-end, come  Adobe Illustrator e  Adobe InDesign. Per ulteriori informazioni, consulta la documentazione fornita con l’applicazione.

Le funzioni di trasferimento sono utilizzate per l&#39;effetto artistico e per regolare le specifiche di un dispositivo di output specifico. Ad esempio, un file destinato all&#39;output su una particolare fotounità può contenere funzioni di trasferimento che compensano il guadagno del punto insito nella stampante.

**Mantieni sottocolore e generazione del nero:** mantiene queste impostazioni se già presenti nel file PostScript. La generazione del nero calcola la quantità di nero da utilizzare quando si tenta di riprodurre un particolare colore. La rimozione del sottocolore (UCR) riduce la quantità di componenti ciano, magenta e giallo per compensare la quantità di nero aggiunta dalla generazione del nero. Poiché utilizza meno inchiostro, UCR è generalmente utilizzato per la carta da giornale e per la carta non patinata.

**Quando vengono trovate le funzioni di trasferimento:** determina cosa fare quando vengono trovate le funzioni di trasferimento:

**Mantieni:** mantiene le funzioni di trasferimento tradizionalmente utilizzate per compensare il guadagno o la perdita di punti che possono verificarsi quando un&#39;immagine viene trasferita su pellicola. Il guadagno del punto si verifica quando i punti di inchiostro che compongono un&#39;immagine stampata sono più grandi (ad esempio, a causa della diffusione su carta) che non nella schermata mezzetinte; la perdita di punti si verifica quando i punti vengono stampati più piccoli. Con questa opzione, le funzioni di trasferimento vengono mantenute come parte del file e applicate al file quando il file viene emesso.

**Applica:** non mantiene la funzione di trasferimento ma la applica al file, che modifica i colori nel file. Questa opzione è utile per creare effetti di colore in un file. Per impostazione predefinita, questa opzione è selezionata per le nuove impostazioni.

**Rimuovi:** rimuove tutte le funzioni di trasferimento applicate. Rimuovere le funzioni di trasferimento applicate, a meno che il file PDF non venga trasmesso sullo stesso dispositivo per il quale è stato creato il file PostScript di origine.

**Mantieni informazioni mezzetinte:** mantiene le informazioni sulle mezzetinte nei file. Le informazioni relative alle mezzetinte sono costituite da punti che controllano la quantità di dispositivi per le mezzetinte di inchiostro che si trovano in una posizione specifica sul foglio. Modificando la dimensione e la densità del punto si crea l’illusione di variazioni di colore grigio o continuo. Per un&#39;immagine CMYK, vengono utilizzati quattro schermi mezzetinte, uno per ogni inchiostro utilizzato nel processo di stampa.

Nella produzione di stampe tradizionali, un&#39;alftonatura viene prodotta posizionando un retino mezzetinte tra un pezzo di pellicola e l&#39;immagine, e quindi esponendo la pellicola. Gli equivalenti elettronici, come in  Adobe Photoshop, consentono agli utenti di specificare gli attributi del retino mezzetinte prima di produrre la pellicola o l&#39;uscita della carta. Le informazioni relative alla mezzatinta sono destinate all’uso con una particolare periferica di output.

## Opzioni avanzate {#advanced-options}

Le opzioni Avanzate specificano i commenti Convenzioni di strutturazione documenti (DSC) da mantenere nel file PDF e come impostare altre opzioni che influiscono sulla conversione da PostScript. In un file PostScript, i commenti DSC contengono informazioni sul file (come l&#39;applicazione di origine, la data di creazione e l&#39;orientamento della pagina). Forniscono inoltre una struttura per le descrizioni delle pagine nel file (come le istruzioni iniziali e finali per una sezione prolog). I commenti DSC possono essere utili quando il documento deve essere stampato o premuto. Per istruzioni su come accedere alle opzioni Avanzate, vedere [Aggiungere o modificare le impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Quando si utilizzano le opzioni Avanzate, è utile conoscere il linguaggio PostScript e come viene tradotto in PDF. (Vedere [ Adobe PostScript 3](https://www.adobe.com/products/postscript/main.html).)

**Consenti al file PostScript di ignorare  impostazioni Adobe PDF:** utilizza le impostazioni memorizzate in un file PostScript invece del file di impostazioni Adobe PDF  corrente. Prima di elaborare un file PostScript, è possibile inserire parametri nel file per controllare i seguenti aspetti:

* compressione di testo e grafica
* downsampling e codifica delle immagini campionate
* incorporazione di font Type 1 e istanze di font Type 1 Multiple Master

**Consenti XObject PostScript:** PostScript XObject memorizzano le informazioni visualizzate su più pagine dello stesso file, ad esempio un&#39;immagine di sfondo o informazioni di intestazione e piè di pagina. L&#39;utilizzo di XObject PostScript può velocizzare la stampa ma richiede più memoria della stampante. Per evitare la creazione di XObject PostScript, deselezionare questa opzione se si creano file PDF con  compatibilità Acrobat 5 (PDF 1.4) o versioni successive.

**Converti sfumature in tonalità omogenee:** converte le fusioni in sfumature uniformi per  Acrobat 4 e versioni successive, riducendo al minimo le dimensioni dei file PDF e migliorando potenzialmente la qualità dell’output finale. PDF Generator converte le sfumature da  Adobe Illustrator,  Adobe InDesign,  Adobe FreeHand MX, CorelDraw, Quark Xpress e Microsoft PowerPoint.

**Converti linee uniformi in curve:** riduce la quantità di punti di controllo utilizzati per creare curve nei disegni CAD, con conseguente riduzione dei file PDF e maggiore velocità di rendering sullo schermo.

**Mantieni semantica di copypage di livello 2:** utilizza l&#39;operatore di copypage definito in PostScript di LanguageLevel 2 anziché in PostScript di LanguageLevel 3. Se disponete di un file PostScript e selezionate questa opzione, un operatore di copypage copia la pagina. Se questa opzione non è selezionata, viene eseguito l&#39;equivalente di un&#39;operazione showpage, ma lo stato grafico non viene reinizializzato.

**Mantieni impostazioni di sovrastampa:** mantiene le impostazioni di sovrastampa nei file da convertire in PDF. I colori sovrastampati sono due o più inchiostri stampati l’uno sull’altro. Ad esempio, quando un inchiostro ciano viene stampato su un inchiostro giallo, la sovrastampa risultante è di colore verde. Senza sovrastampa, il giallo sottostante non viene stampato, generando un colore ciano.

**Sovrastampa predefinita è sovrastampa non zero:** impedisce la sovrastampa di oggetti con valori CMYK pari a zero per l&#39;eliminazione degli oggetti CMYK al di sotto di essi. Questo effetto viene ottenuto inserendo il parametro dello stato grafico OPM 1 nel file PDF ovunque sia presente l&#39;operatore Setoverprint.

**Salva  impostazioni Adobe PDF nel file PDF:** incorpora il file delle impostazioni utilizzato per creare il file PDF. È possibile aprire e visualizzare il file delle impostazioni (con estensione .joboptions) nella finestra di dialogo Allegati file in  Acrobat. Il file delle impostazioni Adobe PDF  diventa un elemento nella struttura File incorporati all’interno del file PDF.

**Salva immagini JPEG originali in PDF Se possibile:** elabora tutte le immagini JPEG compresse (le immagini già compresse con codifica DCT) senza ricomprimerle. Se questa opzione è selezionata, PDF Generator decomprime le immagini JPEG per assicurarsi che non siano danneggiate. Tuttavia, non ricomprime le immagini valide, pertanto l’immagine originale non viene toccata. Con questa opzione selezionata, le prestazioni migliorano perché si verifica solo la decompressione (non la ricompressione) e i dati immagine e metadati vengono conservati.

**Salva biglietto del processo portatile nel file PDF:** mantiene un ticket del processo PostScript in un file PDF. Il ticket di lavoro contiene informazioni sul file PostScript, quali le dimensioni della pagina, la risoluzione e le informazioni di trapping, anziché informazioni sul contenuto. Queste informazioni possono essere utilizzate in un secondo momento in un flusso di lavoro o per stampare il PDF.

**Utilizzate Prolog.ps e Epilog.ps:** invia un file prolog ed epilog con ogni processo. Questi file hanno molti scopi. Ad esempio, i file prolog possono essere modificati per specificare le pagine di copertina. I file Epilog possono essere modificati per risolvere una serie di procedure in un file PostScript. Potete caricare o scaricare i file. Consultate Caricamento e download di file prolog ed epilog.

**Elabora commenti DSC:** mantiene le informazioni DSC da un file PostScript. Sono disponibili le seguenti opzioni secondarie:

**Avvisi DSC di registro:** visualizza messaggi di avviso sui commenti DSC problematici durante l&#39;elaborazione e li aggiunge a un file di registro.

**Mantieni informazioni EPS da DSC:** conserva le informazioni, ad esempio l’applicazione di origine e la data di creazione di un file EPS. Se questa opzione è deselezionata, la pagina viene ridimensionata e centrata in base all&#39;angolo superiore sinistro dell&#39;oggetto superiore sinistro e all&#39;angolo inferiore destro dell&#39;oggetto inferiore destro sulla pagina.

**Mantieni commenti OPI:** conserva le informazioni necessarie per sostituire un&#39;immagine o un commento For Placement Only (FPO) con l&#39;immagine ad alta risoluzione presente sui server che supportano Open Prepress Interface (OPI) versioni 1.3 e 2.0.

**Mantieni informazioni documento da DSC:** conserva informazioni quali titolo, data e ora di creazione. Quando si apre un file PDF in  Acrobat, queste informazioni vengono visualizzate nel pannello Descrizione proprietà documento.

**Ridimensiona pagina e centra immagine per file EPS:** Centra un’immagine EPS e ridimensiona la pagina per adattarla strettamente all’immagine. Questa opzione è valida solo per i processi costituiti da un singolo file EPS.

## Standard, opzioni di reporting e conformità {#standards-reporting-and-compliance-options}

PDF Generator può controllare il contenuto di un documento in un file PostScript per assicurarsi che soddisfi i criteri PDF/X-1a, PDF/X-3 o PDF/A standard prima di creare il file PDF. Per i file compatibili con PDF/X, potete anche richiedere che il file PostScript soddisfi criteri aggiuntivi selezionando altre opzioni in &quot;Reporting and compliance&quot; (Generazione di rapporti e conformità standard). La disponibilità delle opzioni dipende dallo standard selezionato.

I file compatibili con PDF/X vengono utilizzati principalmente come formato standard per lo scambio di file PDF destinati alla produzione di stampe ad alta risoluzione. A meno che non si stia creando un documento PDF per la produzione di stampe, è possibile ignorare gli standard di conformità PDF/X.

I file compatibili con PDF/A vengono utilizzati principalmente per l&#39;archiviazione. Poiché l&#39;obiettivo è la conservazione a lungo termine, il documento deve contenere solo quanto necessario per l&#39;apertura e la visualizzazione per tutta la durata prevista del documento. Ad esempio, i file compatibili con PDF/A possono contenere solo testo, immagini raster e oggetti vettoriali; non possono contenere cifratura e script. Inoltre, tutti i font devono essere incorporati in modo che i documenti possano essere aperti e visualizzati come creati. In altre parole, i documenti conformi allo standard PDF/A sono *più sottili* rispetto ai documenti PDF/X, destinati alla produzione high-end.

>[!NOTE]
>
>se configurate una cartella esaminata per la creazione di file conformi con PDF/A, accertatevi di non aggiungere protezione alla cartella; lo standard PDF/A non consente la cifratura.

Per istruzioni su come accedere alle opzioni di reporting e conformità per gli standard, vedere [Aggiungere o modificare le impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

**Standard di conformità:** selezionate uno standard per produrre un rapporto che indichi se il file è conforme ai requisiti e, in caso contrario, quali problemi sono stati riscontrati. Quando Compatibilità nella pagina Impostazioni generali è impostata su  Acrobat 4.0, sono attivate le seguenti opzioni. Quando Compatibilità è impostata su  Acrobat 5.0, è possibile selezionare solo le opzioni di Acrobat 5.0 . Quando Compatibilità è impostata su un&#39;opzione alternativa, le seguenti opzioni sono disattivate:

* PDF/X-1a (compatibile  Acrobat 4.0)
* PDF/X-3 (compatibile  Acrobat 4.0)
* PDF/X-1a (compatibile  Acrobat 5.0)
* PDF/X-3 (compatibile  Acrobat 5.0)
* PDF/A-1b (compatibile  Acrobat 5.0)

### Opzioni per gli standard PDF/X {#options-for-pdf-x-standards}

**Quando non conforme:** specifica se creare il file PDF se il file PostScript non è conforme ai requisiti PDF/X. Questa opzione è disponibile quando Standard di conformità nella pagina Reporting and Compliance standard è impostata su un&#39;opzione diversa da Nessuno.

**Continua:** crea un file PDF.

**Annulla processo:** crea un file PDF solo se il file PostScript soddisfa i requisiti PDF/X delle opzioni del rapporto selezionate ed è altrimenti valido. Se sono selezionate entrambe le opzioni del rapporto PDF/X e il file PostScript soddisfa solo un set di criteri PDF/X (ad esempio, PDF/X-3), PDF Generator crea il file conforme.

**Se non vengono specificati né TrimBox né ArtBox:** Disponibile quando Standard di conformità nella pagina Reporting and Compliance standard è impostata su un&#39;opzione diversa da Nessuno.

**Rapporto come errore:** contrassegna il file PostScript come non conforme se è selezionata una delle opzioni di reporting e manca una casella di rifilo o una casella grafica in una qualsiasi pagina.

**Imposta TrimBox su MediaBox con offset:** calcola i valori in punti per la casella di rifilo in base agli offset per la casella del supporto delle rispettive pagine, se non sono specificati né il riquadro di rifilo né il riquadro della grafica. La casella di rifilo è sempre piccola o più piccola della casella del supporto.

**Se BleedBox non è specificato:** Disponibile quando Standard di conformità nella pagina Reporting and Conformità standard è impostata su un&#39;opzione diversa da Nessuno.

**Imposta BleedBox su MediaBox:** utilizza i valori della casella di riepilogo dei file multimediali per la casella di pagina al vivo se la casella di pagina al vivo non è specificata.

**Imposta BleedBox su TrimBox con offset:** calcola i valori in punti per la casella di pagina al vivo in base agli offset per la casella di rifilo delle rispettive pagine, se la casella di pagina al vivo non è specificata. La casella di pagina al vivo è sempre grande o più grande della casella di rifilo racchiusa.

**Valori predefiniti Se Non specificato nel documento:** questa opzione è disponibile quando Standard di conformità nella pagina Reporting and Compliance standard è impostata su un&#39;opzione diversa da Nessuno.

**Nome profilo intento di output:** indica la condizione di stampa caratterizzata per la quale il documento è preparato. Se un documento non specifica un nome OutputIntent, PDF Generator utilizza il valore selezionato da questo menu. È possibile selezionare uno dei nomi forniti oppure immettere un nome nello spazio disponibile. Se il flusso di lavoro richiede che il documento specifichi l&#39;intento di output, selezionare Nessuno. I documenti che non soddisfano i requisiti non superano il controllo di conformità.

**Identificatore condizione di output:** indica il nome di riferimento specificato dal Registro di sistema del nome del profilo dell&#39;intento di output.

**Condizione di output:** Descrive la condizione di stampa desiderata. Questa voce può essere utile per il destinatario previsto del documento PDF.

**Nome del Registro di sistema (URL):** indica l’indirizzo Web per ulteriori informazioni sul Registro di sistema. L’URL viene immesso automaticamente per i nomi del Registro di sistema ICC.

**Trapping:** indica lo stato del trapping nel documento. La conformità PDF/X richiede il valore True o False. Se il documento non specifica lo stato di intrappolamento, viene utilizzato il valore fornito qui. Se il flusso di lavoro richiede che il documento specifichi lo stato di intrappolamento, selezionare Lascia non definito. I documenti che non soddisfano i requisiti non superano il controllo di conformità.

### Opzioni per lo standard PDF/A {#options-for-pdf-a-standard}

Queste opzioni sono attivate quando Compatibilità (nell’area Generale) è impostata su  Acrobat 4 (PDF 1.3) o  Acrobat 5 (PDF 1.4).

**Quando non conforme:** specifica se creare il file PDF se il file PostScript non è conforme ai requisiti PDF/A.

**Continua:** crea un file PDF anche se il file PostScript non soddisfa i requisiti dello standard.

**Annulla processo:** crea un file PDF solo se il file PostScript soddisfa i requisiti PDF/A e per il resto è valido.

**Nome profilo intento di output:** indica la condizione di stampa caratteristica per la quale il documento è stato preparato ed è necessaria per la conformità PDF/A. Se il flusso di lavoro richiede che il documento specifichi le informazioni sull&#39;intento di output, selezionare &quot;None&quot;. Il controllo della conformità del documento non verrà eseguito correttamente se tali informazioni non vengono fornite.

**Condizione di output:** Descrive la condizione di stampa desiderata. Questa voce non è obbligatoria, ma può essere utilizzata per fornire informazioni utili al destinatario previsto del documento PDF.

## Opzioni di visualizzazione iniziali {#initial-view-options}

Queste opzioni sono organizzate in tre aree: Opzioni documento, finestra e interfaccia utente. Per istruzioni su come accedere alle opzioni di visualizzazione Iniziale, vedere [Aggiungere o modificare le impostazioni PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Per utilizzare qualsiasi opzione, selezionare Imposta impostazioni vista iniziale.

### Opzioni documento {#document-options}

Le opzioni del documento controllano l&#39;aspetto del documento all&#39;interno della finestra del documento, ad esempio il livello di ingrandimento e la modalità di scorrimento.

**Mostra:** determina per impostazione predefinita i riquadri e le schede visualizzati nella finestra dell&#39;applicazione. Pannello Segnalibri e Pagina apre il riquadro del documento e visualizza la scheda Segnalibri.

**Layout di pagina:** determina se il documento viene visualizzato in modalità pagina singola, pagina fronte, pagina continua o pagina fronte/retro.

**Ingrandimento:** imposta il livello di zoom utilizzato per visualizzare il documento quando viene aperto. Per impostazione predefinita viene utilizzato il valore di ingrandimento configurato dall’utente nelle preferenze  di Acrobat o  Adobe Reader.

**Apri in numero pagina:** imposta la pagina in cui si apre il documento, che in genere corrisponde alla pagina 1.

>[!NOTE]
>
>L&#39;impostazione Predefinita per le opzioni di ingrandimento e layout di pagina utilizza le singole impostazioni utente nelle preferenze Visualizzazione pagina  Acrobat o  Adobe Reader.

### Opzioni finestra {#window-options}

Le opzioni della finestra determinano il modo in cui la finestra si regola nell&#39;area dello schermo quando un utente apre il documento. Tuttavia, le opzioni non hanno alcun effetto quando un documento PDF viene visualizzato all’interno di un browser Web.

**Ridimensiona finestra alla pagina iniziale:** regola la finestra del documento per adattarla lentamente alla pagina iniziale, in base alle opzioni selezionate in Opzioni documento.

**Centra finestra sullo schermo:** posiziona la finestra al centro dell&#39;area dello schermo.

**Apri in modalità Schermo intero:** consente di ingrandire la finestra del documento e di visualizzare il documento senza i controlli della barra dei menu, della barra degli strumenti o della finestra.

**Mostra:** Nome file mostra il nome del file nella barra del titolo della finestra. Il titolo del documento mostra il titolo del documento nella barra del titolo della finestra.

### Opzioni interfaccia utente {#user-interface-options}

Le opzioni dell&#39;interfaccia utente determinano quali controlli vengono visualizzati o nascosti quando l&#39;utente apre il documento.

**Nascondi barra dei menu:** se selezionata, nasconde la barra dei menu

**Nascondi barre degli strumenti:** se questa opzione è selezionata, nasconde le barre degli strumenti

**Nascondi controlli finestra:** se selezionata, nasconde i controlli della finestra

>[!NOTE]
>
>Se si nascondono la barra dei menu e la barra degli strumenti, gli utenti non possono applicare comandi e selezionare strumenti a meno che non siano a conoscenza delle scelte rapide da tastiera quando aprono il file in  Acrobat.

## Caricamento e download di file prolog ed epilog {#uploading-and-downloading-prologue-and-epilogue-files}

I file Prolog vengono utilizzati per aggiungere codice PostScript personalizzato che viene eseguito all&#39;inizio di ogni processo PostScript in fase di distillazione. I file Epilog vengono utilizzati per aggiungere codice PostScript personalizzato che viene eseguito alla fine di ogni processo PostScript. Potete scaricare i file prolog ed epilog dal server per salvarli localmente. È possibile scaricare i file per configurarli in modo indipendente o per caricarli in un&#39;altra posizione o in un altro computer.

Questi file hanno molti scopi. Ad esempio, i file prolog possono essere modificati per specificare le pagine di copertina; i file epilog possono essere modificati per risolvere una serie di procedure in un file PostScript. Potete anche selezionare e caricare i file prolog ed epilog da inviare con ogni processo.

### Scaricare un file prolog o epilog {#download-a-prologue-or-epilogue-file}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator >  Impostazioni Adobe PDF.
1. Fate clic su Nuovo o sul nome di un’impostazione.
1. Fate clic su Avanzate, quindi, accanto all’opzione Usa Prolog.ps e Epilog.ps, fate clic su Scarica.
1. Nella pagina Download Prolog e File Epilog, fate clic su Prolog.ps o Epilog.ps e fate clic su Salva.

### Caricare un file prolog o epilog {#upload-a-prologue-or-epilogue-file}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator >  Impostazioni Adobe PDF.
1. Fate clic su Nuovo o sul nome di un’impostazione.
1. Fate clic su Avanzate, quindi, accanto all’opzione Usa Prolog.ps e Epilog.ps, fate clic su Carica.
1. Nella pagina Carica file prolog ed Epilog, fate clic su Sfoglia per selezionare un file prolog o epilog.
1. Individuate il file e fate clic su Apri.
1. Per utilizzare il file, accertatevi che l&#39;opzione Usa Prolog.ps e Epilog.ps sia selezionata nell&#39;area Avanzate della pagina Nuova/Modifica impostazione Adobe PDF .
1. Fai clic su Salva

>[!NOTE]
>
>PDF Generator supporta i file prolog ed epilog solo per la conversione di file PostScript e PostScript incapsulati in PDF.

