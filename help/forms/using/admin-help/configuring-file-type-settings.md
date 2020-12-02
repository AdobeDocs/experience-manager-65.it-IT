---
title: Configurazione delle impostazioni del tipo di file
seo-title: Configurazione delle impostazioni del tipo di file
description: Scoprite come configurare le impostazioni del tipo di file.
seo-description: Scoprite come configurare le impostazioni del tipo di file.
uuid: ab037659-c6ff-4de9-9417-f5a6fc8122cb
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ab19b248-8931-4cf6-b6a5-fb7b067c4a49
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '6146'
ht-degree: 2%

---


# Configurazione delle impostazioni dei tipi di file {#configuring-file-type-settings}

In PDF Generator, è possibile impostare le impostazioni dell&#39;applicazione per i tipi di file supportati. In Windows, potete impostare le impostazioni dell&#39;applicazione per ciascun tipo di file supportato. In UNIX e Linux, potete impostare le impostazioni dell&#39;applicazione per HTML-to-PDF e OpenOffice.

Nella pagina Impostazioni tipo di file è possibile eseguire le seguenti operazioni:

* [Creare o modificare un&#39;impostazione Tipo di file](#create-or-edit-file-type-settings)
* Specificare le impostazioni del tipo di file da utilizzare per impostazione predefinita (vedere [Importazione ed esportazione di file di configurazione PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md))
* [Modificare le impostazioni predefinite](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)
* [Abilita supporto PDF/A](/help/forms/using/admin-help/enable-pdf-a-support.md)
* [Eliminare un&#39;impostazione Tipo di file](/help/forms/using/admin-help/enable-pdf-a-support.md)

>[!NOTE]
>
>Le impostazioni relative al tipo di file non sono disponibili per i convertitori di fallback, come  Acrobat per la conversione da HTML a PDF, Microsoft PowerPoint, Microsoft Word e Microsoft Excel.

## Creare o modificare le impostazioni del tipo di file {#create-or-edit-file-type-settings}

Creare o modificare un&#39;impostazione di tipo di file per specificare come l&#39;applicazione gestisce la conversione dei tipi di file supportati. In Windows, potete impostare le impostazioni dell&#39;applicazione per ciascun tipo di file supportato. In UNIX e Linux, potete impostare le impostazioni dell&#39;applicazione per HTML-to-PDF e OpenOffice.

1. Nella console di amministrazione, fare clic su **[!UICONTROL Services]** > **[!UICONTROL PDF Generator]** > **[!UICONTROL File Type Settings]**.
1. Fate clic su Nuovo o sul nome di un’impostazione.
1. Nella casella Estensioni nome file digitare le estensioni del nome file, separate da virgole, per i tipi di file accettati per l&#39;applicazione. Non includete il punto precedente o uno spazio tra le estensioni. Il valore predefinito è `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Facoltativo) Per utilizzare il riconoscimento ottico del codice (OCR) del testo negli elementi grafici o nelle immagini, selezionare Usa OCR e impostare le seguenti opzioni:

**Lingua OCR principale:** la lingua utilizzata dal motore OCR per identificare i caratteri. Il valore predefinito è Inglese (USA).

**Stile output PDF:** selezionate Immagine ricercabile per ottenere un’immagine bitmap delle pagine in primo piano e del testo acquisito su un livello invisibile al di sotto. L&#39;aspetto della pagina non cambia, ma il testo diventa selezionabile e leggibile. Selezionate Testo formattato e grafica per ricostruire la pagina originale utilizzando testo, font, immagini e altri elementi grafici riconosciuti. Il valore predefinito è Immagine ricercabile (Esatto).

**Immagini sottocampionate:** riduce il numero di pixel per immagini a colori, in scala di grigi e monocromatiche. Il downsampling delle immagini scansionate viene eseguito al termine dell&#39;OCR. Il valore predefinito è Più basso (600 dpi). Questa opzione non è disponibile se lo stile di output PDF è impostato su Immagine ricercabile (Esatto).

1. Compila le informazioni richieste nelle seguenti sezioni:

   [Importazione ed esportazione di file di configurazione PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)

   [ le impostazioni di esportazione Adobe PDF (solo Windows)](#adobe-pdf-export-settings-windows-only)

   [Impostazioni HTML-PDF](#html-to-pdf-settings)

   [Flash video alle impostazioni PDF](#flash-videos-to-pdf-settings)

   [Impostazioni da XPS a PDF](#xps-to-pdf-settings)

   [Impostazioni di ottimizzazione PDF](/help/forms/using/admin-help/configuring-file-type-settings.md)

   [Impostazioni di Microsoft Excel (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-excel-settings-windows-only)

   [Impostazioni di Microsoft PowerPoint (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-powerpoint-settings-windows-only)

   [Impostazioni Microsoft Project (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-project-settings-windows-only)

   [Impostazioni di Microsoft Word (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-word-settings-windows-only)

   [Impostazioni di Microsoft Visio (solo Windows)](#visio)

   [Impostazioni di Microsoft Publisher (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-publisher-settings-windows-only)

   [Impostazioni AutoCAD (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#autocad-settings-windows-only)

   [Impostazioni OpenOffice](/help/forms/using/admin-help/configuring-file-type-settings.md#openoffice-settings)

   [Impostazioni di altre applicazioni (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#other-applications-settings-windows-only)

   Per passare a un&#39;altra sezione, fare clic sul relativo collegamento sulla pagina Web o utilizzare i pulsanti **[!UICONTROL Next]** o **[!UICONTROL Previous]**.

1. Dopo aver completato tutte le sezioni, fare clic su **[!UICONTROL Salva]** o **[!UICONTROL Salva con nome]** e specificare un nome per l&#39;impostazione.

È possibile personalizzare il supporto per diversi tipi di file. (Vedere &quot; [Aggiunta del supporto per formati di file nativi aggiuntivi](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot; in [Programmazione con moduli AEM](https://www.adobe.com/go/learn_lc_programming_11).)

## Modificare le impostazioni predefinite {#change-the-default-settings}

È possibile modificare il valore predefinito per le impostazioni di  Adobe PDF, le impostazioni di protezione e il tipo di file che si applicano alle origini appena create. La modifica delle impostazioni predefinite non influisce sulle impostazioni delle origini esistenti.

1. In Admin Console, fare clic su **[!UICONTROL Servizi > PDF Generator]**.
1. Nella pagina **[!UICONTROL Adobe PDF Settings]**, **[!UICONTROL File Type Settings]** o **[!UICONTROL Security Settings]** fare clic su **[!UICONTROL Set Default Settings]** (Imposta impostazioni predefinite).
1. Selezionate le impostazioni predefinite preferite. Nella pagina Imposta impostazioni predefinite è disponibile una o più delle seguenti impostazioni:

   **[!UICONTROL impostazione]** Adobe PDF: Il valore predefinito originale è Standard ( Acrobat 6).

   **[!UICONTROL Impostazioni]** di protezione: Il valore predefinito originale è Nessuna protezione ( Acrobat 5).

   **[!UICONTROL Impostazioni]** tipo di file: Il valore predefinito originale è Standard.

1. Fai clic su **[!UICONTROL Salva]**.

## Elimina l&#39;impostazione Tipo file {#delete-a-file-type-setting}

È possibile eliminare un&#39;impostazione di tipo di file non più utilizzata.

1. Nella console di amministrazione, fare clic su **[!UICONTROL Servizi > Generatore PDF> Impostazioni tipo di file]**.
1. Selezionate la casella accanto all’impostazione da eliminare. Potete selezionare più origini. Le impostazioni a cui non è associata una casella di controllo sono sempre incluse con PDF Generator e non possono essere eliminate.
1. Fare clic su **[!UICONTROL Elimina]** e, nella pagina Elimina conferma, fare clic su **[!UICONTROL Elimina]**.

## Impostazioni di Image to PDF {#image-to-pdf-settings}

Le seguenti opzioni determinano il modo in cui i file immagine vengono convertiti in PDF. Per istruzioni su come accedere a queste impostazioni, vedere [Creare o modificare le impostazioni dei tipi di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Estensioni nome file: elenco separato da** virgole di estensioni di nomi file convertibili.

**Prova Fallback Converter:** PDF Generator può usare Java™ o  Acrobat per convertire i file immagine in PDF. Quando questa opzione è selezionata e una conversione non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando il metodo alternativo. Se il metodo alternativo non riesce o raggiunge il limite di timeout specificato, nel file di registro viene scritta un&#39;eccezione.

>[!NOTE]
>
>I file JPEG 2000 possono essere convertiti solo utilizzando  Acrobat.

**Usa OCR:** specifica se applicare l&#39;OCR (riconoscimento ottico dei caratteri) al PDF. Il software OCR consente di cercare, correggere e copiare il testo nel PDF.

***nota **: La funzione PDF OCR (PDF ricercabile) è supportata solo in Microsoft Windows.*

**Lingua OCR principale:** specifica la lingua da utilizzare per identificare i caratteri nel motore OCR.

**Stile output PDF:** determina il tipo di file PDF da produrre. Tutti i formati applicano il riconoscimento OCR e il riconoscimento dei font e della pagina alle immagini di testo e li convertono in testo normale.

**Immagine ricercabile:** assicura che il testo sia ricercabile e selezionabile. Questa opzione consente di mantenere l’immagine originale, desktop in base alle esigenze e vi colloca sopra un livello di testo invisibile. L’opzione Downsampling immagini determina se l’immagine viene ricampionata e in quale misura.

**Immagine ricercabile (Esatto):** assicura che il testo sia ricercabile e selezionabile. Questa opzione mantiene l’immagine originale e vi colloca sopra un livello di testo invisibile. Consigliato per i casi che richiedono la massima fedeltà all’immagine originale.

**ClearScan:** sintetizza un nuovo font Type 3 che avvicina strettamente l&#39;originale e mantiene lo sfondo della pagina utilizzando una copia a bassa risoluzione.

**Downsampling immagini:** riduce il numero di pixel nelle immagini a colori, in scala di grigio e monocromatiche al termine dell’OCR. Scegliete il grado di downsampling da applicare. Le opzioni numerate più elevate consentono di eseguire meno il downsampling, producendo quindi PDF a risoluzione più elevata.

##  impostazioni di esportazione Adobe PDF (solo Windows) {#adobe-pdf-export-settings-windows-only}

L&#39;impostazione Tipo file esportazione nella sezione  impostazioni di esportazione Adobe PDF viene utilizzata per convertire un file PDF in un altro formato. Il valore predefinito è HTML 4.01 con fogli di stile CSS 1.0 (*.htm, *.html).

Per istruzioni su come accedere a questa impostazione, vedere [Creare o modificare le impostazioni dei tipi di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Impostazioni HTML-PDF {#html-to-pdf-settings}

Le seguenti opzioni determinano la modalità di conversione dei file HTML in PDF. Per istruzioni su come accedere a queste opzioni, vedere [Creare o modificare le impostazioni dei tipi di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Prova Fallback Converter:** PDF Generator può usare Java™ o  Acrobat per convertire i file HTML in PDF. Quando questa opzione è selezionata e una conversione non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando il metodo alternativo. Se il metodo alternativo non riesce o raggiunge il limite di timeout specificato, nel file di registro viene scritta un&#39;eccezione.

**Codifica predefinita:** imposta la codifica di input del testo del file da un menu di sistemi operativi e alfabeti. Utilizza la selezione visualizzata nell&#39;opzione Codifica predefinita solo se il file di origine HTML non specifica un tipo di codifica.

**Forza codifica selezionata:** ignora qualsiasi codifica specificata nel file di origine HTML e utilizza la selezione mostrata nell&#39;opzione Codifica predefinita.

### Impostazioni di spiaggiatura {#spidering-settings}

** Spideringanalizza le pagine Web per i collegamenti ad altre pagine Web. Quando viene rilevato un collegamento a un&#39;altra pagina Web, la pagina di destinazione viene recuperata e inclusa nel documento PDF generato. Abilitate queste opzioni per impostare il numero di livelli da recuperare e convertire in PDF:

**Ottieni solo livelli X:** Ragni e converte le pagine fino a una profondità del livello specificato dall’URL della pagina di base. Un valore pari a 1 converte solo l’URL fornito.

**Ottieni intero sito:** converte l’intero sito, a partire dall’URL fornito.

**Stesso percorso:** tutti i collegamenti che fanno riferimento a pagine che non si trovano sullo stesso percorso relativo dell&#39;URL di base non vengono convertiti durante il ragionamento.

**Soggiorno sullo stesso server:** tutti i collegamenti che puntano alle pagine su server diversi non vengono convertiti durante il ragionamento. Vengono convertiti solo i collegamenti che puntano allo stesso server dell&#39;URL specificato.

### Impostazioni di conversione delle pagine {#page-conversion-settings}

Abilitate queste opzioni per specificare la modalità di conversione delle pagine HTML. In base alle dimensioni della pagina, i valori di larghezza, altezza e margine si regolano di conseguenza.

**Dimensioni pagina:** scegliete un’opzione personalizzata e specificate la larghezza e l’altezza, oppure selezionate dimensioni predefinite.

**Orientamento:** selezionare verticale o orizzontale per il documento PDF convertito.

**Margini:** specifica i margini (In alto, In basso, A sinistra e A destra) del documento PDF generato.

**Aggiungi segnalibri al PDF:** aggiunge segnalibri al documento PDF.

**Abilita PDF con tag:** incorpora i tag nel documento PDF.

**Impostazioni vista iniziale:** consente di configurare le opzioni Documento, Finestra e Interfaccia utente. Queste impostazioni determinano il modo in cui il contenuto viene visualizzato inizialmente.

### Opzioni documento {#document-options}

Abilitare queste opzioni per specificare come visualizzare il contenuto, come visualizzare le pagine nel documento PDF e come specificare il livello di ingrandimento:

**Mostra:** selezionare i riquadri da aprire in  Acrobat all&#39;apertura del documento PDF.

**Layout pagina:** selezionare il tipo di layout di pagina per il documento PDF.

**Ingrandimento:** scegliete l’ingrandimento predefinito per la visualizzazione iniziale del documento PDF o selezionate un valore personalizzato. Se si sceglie un&#39;impostazione predefinita, viene usata l&#39;ingrandimento  Acrobat predefinito.

**Apri in numero pagina:** specificare il numero di pagina a cui si apre il PDF.

### Opzioni finestra {#window-options}

Abilitate queste opzioni per specificare le dimensioni e la visualizzazione della finestra.

**Ridimensiona finestra alla pagina iniziale:** ridimensiona la finestra Acrobat  alle dimensioni della pagina iniziale.

**Centra finestra sullo schermo:** apre la finestra al centro dello schermo.

**Apri in modalità Schermo intero:** apre la finestra in modalità Schermo intero.

**Mostra:** visualizza il titolo o il nome del documento nella finestra.

### Opzioni interfaccia utente {#user-interface-options}

Abilitate queste opzioni per specificare l’aspetto della finestra:

**Nascondi barra dei menu:** nasconde la barra dei menu nel documento PDF.

**Nascondi barre degli strumenti:** nasconde le barre degli strumenti nel documento PDF.

**Nascondi controlli finestra:** nasconde i controlli della finestra nel documento PDF.

## Flash video alle impostazioni PDF {#flash-videos-to-pdf-settings}

PDF Generator supporta la possibilità di inviare un video per  Flash Adobe (file SWF o FLV) e creare un file PDF con un video per  Flash Adobe incorporato al suo interno. Questa conversione non richiede l&#39;installazione  Flash Player Adobe nel server dei moduli. Per istruzioni su come accedere a questa opzione, vedere [Creare o modificare le impostazioni dei tipi di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Estensioni nome file: elenco separato da** virgole di estensioni di nomi file convertibili.

## Impostazioni XPS - PDF {#xps-to-pdf-settings}

XML Paper Specification (XPS) è utilizzato nella macchina di stampa Windows. Questo è un formato Microsoft e può essere creato da qualsiasi applicazione di Microsoft Office. AEM moduli consente di convertire file XPS in formato PDF.

**Estensioni nome file:** elenco separato da virgole di tutte le estensioni del nome file XPS che è possibile convertire. Attualmente esiste un formato: .xps.

## Impostazioni di ottimizzazione PDF {#pdf-optimizer-settings}

PDF Generator supporta la possibilità di ridurre le dimensioni dei file PDF. L’utilizzo di tutte queste impostazioni o solo di alcune dipende da come intendete utilizzare i file e dalle proprietà essenziali che un file deve avere. Nella maggior parte dei casi, le impostazioni predefinite sono adatte alla massima efficienza, consentendo di risparmiare spazio rimuovendo i font incorporati, comprimendo le immagini e rimuovendo elementi dai file che non sono più necessari.

>[!NOTE]
>
>L&#39;ottimizzazione di un documento con firma digitale rimuove e invalida le firme digitali.

Per istruzioni su come accedere a questa impostazione, vedere [Creare o modificare le impostazioni dei tipi di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Versione PDF di destinazione:** specifica la versione di  Acrobat con cui il PDF è compatibile.

### Font {#fonts}

1. Selezionare **Font.**
1. Selezionare una delle seguenti opzioni:

   **Scorpora tutti i font:** Sincorpora tutti i font incorporati.

   **Non incorporare alcun font:** non incorpora alcun font.

   **Scorpora alcuni font:** Sincorpora solo i font specificati. Per specificare i font da annullare l’incorporazione, effettuate le seguenti operazioni:

   * Se necessario, selezionate una directory di font diversa dal menu a discesa **Font source**. Questo menu a discesa elenca le directory dei font specificate in **Home > Impostazioni > Sistema di base > Configurazioni di base**.
   * Selezionare uno o più font dall&#39;elenco **Font disponibili** e fare clic su **Aggiungi**. Questi font vengono aggiunti all&#39;elenco **Font a Unembed**.
   * Se si desidera rimuovere alcuni font che non esistono nel server dei moduli, immettere i nomi di tali font nella casella **Aggiungi font a unembed**. Fate clic su **Aggiungi**.

   >[!NOTE]
   >
   >*Se si desidera rimuovere alcuni font i cui sottoinsiemi sono incorporati nel documento, aggiungere il prefisso al nome del font con il segno +. Ad esempio, &quot;+Helvetica&quot;.*

1. Se si desidera incorporare solo i sottoinsiemi in uso dei font incorporati, selezionare **Sottoinsiemi tutti i font incorporati**.

   >[!NOTE]
   >
   >*Se utilizzate questa opzione insieme ad **Unembed alcuni font**, i font inclusi nell&#39;elenco **Aggiungi font a**unembedlist rimangono completamente non incorporati.*

   >[!NOTE]
   >
   >*Il sottoinsieme di font è la tecnica per incorporare solo una parte di un font. Un sottoinsieme di font contiene solo i caratteri utilizzati nel documento.*

### Trasparenza {#transparency}

Se il documento PDF include immagini con trasparenza, è possibile utilizzare le impostazioni Ottimizzatore PDF per appiattire la trasparenza e ridurre le dimensioni del file.

>[!NOTE]
>
>Se  Acrobat 4.0 e versioni successive è selezionato come versione PDF di destinazione, tutti gli oggetti trasparenti vengono appiattiti. Per le altre versioni PDF di Target, la trasparenza è supportata e potete configurare le impostazioni di trasparenza.

Selezionare **Trasparenza** per configurare le impostazioni di trasparenza durante l&#39;ottimizzazione dei documenti PDF.

**Livello** di trasparenza: consente di specificare la quantità di informazioni vettoriali da mantenere. Con impostazioni più elevate vengono mantenuti più oggetti vettoriali, mentre con impostazioni più basse vengono rasterizzati più oggetti vettoriali; le impostazioni intermedie consentono di preservare le aree semplici sotto forma di vettore e di rasterizzare quelle complesse. Selezionate l’impostazione più bassa per rasterizzare tutta la grafica.

>[!NOTE]
>
>La quantità di rasterizzazione che si verifica dipende dalla complessità della pagina e dai tipi di oggetti sovrapposti.

**Line Art e** TextResolution a cui vengono rasterizzati tutti gli oggetti, incluse immagini, grafica vettoriale, testo e sfumature. I valori supportati sono da 1 pixel per pollice (ppi) a 9600 ppi.

>[!NOTE]
>
>La risoluzione Art. linea e Testo deve essere generalmente impostata su 600-1200 ppi per garantire una rasterizzazione di alta qualità, in particolare per il tipo serif o di piccole dimensioni.

**Sfumatura e** trameRisoluzione a cui vengono rasterizzate sfumature e trame. I valori supportati sono compresi tra 1 e 1200 ppi.

>[!NOTE]
>
>La risoluzione della sfumatura e della trama deve essere generalmente impostata su 150-300 ppi, perché la qualità delle sfumature, delle ombre esterne e delle piume non migliora con risoluzioni più elevate, ma il tempo di stampa e la dimensione del file aumentano.

**Converti tutto il testo in** contorniConverte tutti gli oggetti di tipo (tipo di punto, tipo di area e tipo di percorso) in contorni e scarta tutte le informazioni di tipo glifo nelle pagine contenenti trasparenza. Questa opzione assicura che la larghezza del testo rimanga costante durante la conversione. Se si attiva questa opzione, i font di piccole dimensioni verranno visualizzati leggermente più spessi se visualizzati in  Acrobat o stampati con stampanti desktop a bassa risoluzione. Non influisce sulla qualità del tipo stampato su stampanti o fotounità ad alta risoluzione.

**Converti tutti i tratti in** contorniConverte tutti i tratti in semplici tracciati riempiti su pagine contenenti trasparenza. Questa opzione assicura che la larghezza dei tratti rimanga costante durante la conversione. Tenete presente che l’attivazione di questa opzione fa sì che i tratti sottili appaiano leggermente più spessi e potrebbero compromettere le prestazioni di appiattimento.

**Ritaglia** aree complesse: consente di definire i bordi tra grafica vettoriale e grafica rasterizzata lungo i percorsi degli oggetti. Questa opzione consente di ridurre gli artefatti che si verificano quando parte di un og

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Alcuni driver di stampa elaborano la grafica raster e vettoriale in modo diverso, producendo talvolta cuciture a colori. È possibile ridurre al minimo i problemi di cucitura disattivando alcune impostazioni di gestione del colore specifiche per i driver di stampa. Queste impostazioni variano a seconda della stampante, per ulteriori informazioni consultare la documentazione fornita con la stampante.

Mantieni sovrastampa: Consente di fondere il colore della grafica trasparente con il colore di sfondo per creare un effetto di sovrastampa.

La tabella seguente mostra i tipi comuni di stampanti e la loro risoluzione, misurata in dpi, la loro risoluzione predefinita dello schermo misurata in linee per pollice (lpi) e una risoluzione di ricampionamento per le immagini misurata in pixel per pollice (ppi). Ad esempio, se steste stampando su una stampante laser a 600 dpi, immettete 170 per la risoluzione a cui campionare le immagini.

**** Immagini: selezionate Immagini per specificare le opzioni di compressione e ricampionamento per le immagini a colori, in scala di grigi e monocromatiche. È possibile provare a utilizzare queste opzioni per trovare un equilibrio appropriato tra la dimensione del file e la qualità dell&#39;immagine.L&#39;impostazione di risoluzione per le immagini a colori e in scala di grigio dovrebbe essere 1,5-2 volte superiore alla schermata della linea in cui il file verrà stampato. La risoluzione per le immagini monocromatiche dovrebbe essere la stessa della periferica di output, ma tenete presente che il salvataggio di un&#39;immagine monocromatica a una risoluzione superiore a 1500 dpi aumenta le dimensioni del file senza migliorare sensibilmente la qualità dell&#39;immagine. Le immagini che verranno ingrandite, come le mappe, potrebbero richiedere risoluzioni più elevate.

>[!NOTE]
>
>Il ricampionamento delle immagini monocromatiche può produrre risultati di visualizzazione imprevisti, ad esempio nessuna visualizzazione delle immagini. In questo caso, disattivate il ricampionamento e convertite di nuovo il file. Questo problema si verifica con maggiore probabilità con il sottocampionamento e con minore probabilità con il downsampling bicubico.

<table>
 <tbody>
  <tr>
   <th><p><strong>Risoluzione della stampante</strong></p> </th>
   <th><p><strong>Schermata di linea predefinita</strong></p> </th>
   <th><p><strong>Risoluzione delle immagini</strong></p> </th>
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

#### Elimina oggetti {#discard-objects}

* Selezionare **Elimina oggetti** per specificare gli oggetti da rimuovere dal PDF e per ottimizzare le linee curve nei disegni CAD.
* **Elimina Tutte Le Azioni** Di Invio, Importazione E Reimpostazione Del Modulo: Disattiva tutte le azioni relative all&#39;invio o all&#39;importazione dei dati del modulo e ripristina i campi del modulo. Questa opzione mantiene gli oggetti modulo a cui sono collegate le azioni.
* **Elimina tutte le azioni** JavaScript: Rimuove dal PDF tutte le azioni che utilizzano JavaScript.
* **Elimina miniature** pagina incorporate: Rimuove le miniature di pagina incorporate. Questa opzione è utile per i documenti di grandi dimensioni, che possono richiedere molto tempo per disegnare le miniature di pagina dopo aver fatto clic sul pulsante Pagine.
* **Converti linee smussate in curve**: Riduce il numero di punti di controllo utilizzati per creare curve nei disegni CAD, con conseguente riduzione dei file PDF e maggiore velocità di rendering sullo schermo.
* **Elimina impostazioni** di stampa incorporate: Rimuove dal documento le impostazioni di stampa incorporate, come il ridimensionamento della pagina e la modalità fronte/retro.
* **Elimina segnalibri**: Rimuove tutti i segnalibri dal documento.
* **Campi** modulo appiattiti: Rende i campi modulo inutilizzabili senza modificarne l’aspetto. I dati del modulo vengono uniti alla pagina per diventare contenuto della pagina.
* **Elimina tutte le immagini** alternative: Rimuove tutte le versioni di un’immagine tranne quella destinata alla visualizzazione a schermo. Alcuni PDF includono più versioni della stessa immagine per diversi scopi, ad esempio la visualizzazione a bassa risoluzione sullo schermo e la stampa ad alta risoluzione.
* **Elimina tag** documento: Rimuove i tag dal documento, rimuovendo in tal modo anche le funzionalità di accesso facilitato e ridisposizione del testo.
* **Rileva E Unisci Frammenti** Immagine: Cerca immagini o maschere frammentate in sezioni sottili e tenta di unire le sezioni in un’unica immagine o maschera.
* **Elimina indice** di ricerca incorporato: Rimuove gli indici di ricerca incorporati, riducendo le dimensioni del file.

#### Elimina dati utente {#discard-user-data}

Selezionare **Elimina dati utente** per rimuovere eventuali informazioni personali che non si desidera distribuire o condividere con altri utenti.

* **Elimina Tutti I Commenti, Forms E File Multimediali**: Rimuove dal PDF tutti i commenti, moduli, campi modulo e contenuti multimediali.
* **Elimina tutti i dati** oggetto: Rimuove tutti gli oggetti dal PDF.
* **Elimina riferimenti** incrociati esterni: Rimuove i collegamenti ad altri documenti. I collegamenti che consentono di passare ad altre posizioni all’interno del PDF non vengono rimossi.
* **Elimina Contenuto Livello Nascosto E Appiattisci Livelli** Visibili: Diminuisce la dimensione del file. Il documento ottimizzato è simile al PDF originale ma non contiene informazioni sul livello.
* **Elimina Informazioni Documento E Metadati**: Rimuove le informazioni nel dizionario delle informazioni del documento e in tutti i flussi di metadati. Per ripristinare i flussi di metadati a una copia del PDF, usate il comando Salva con nome.
* **Elimina allegati** file: Rimuove tutti gli allegati di file, inclusi gli allegati aggiunti al PDF come commenti. PDF Optimizer non ottimizza i file allegati.
* **Elimina Dati Privati Di Altre Applicazioni**: Elimina le informazioni da un documento PDF utili solo per l&#39;applicazione che ha creato il documento. Questa impostazione non influisce sulle funzionalità del PDF, ma riduce le dimensioni del file.

### Pulizia {#clean-up}

Selezionare **Pulisci** per rimuovere elementi non necessari dal documento.
Tali elementi includono elementi obsoleti o non necessari per l&#39;uso previsto del documento. La rimozione di alcuni elementi può seriamente compromettere la funzionalità del PDF. Per impostazione predefinita, sono selezionati solo gli elementi che non influiscono sulla funzionalità. Se non si è certi delle implicazioni della rimozione di altre opzioni, utilizzare le selezioni predefinite.

**Compressione**

Selezionate una delle seguenti opzioni di compressione Flate dal menu a discesa:

* Comprimi file intero
* Comprimi struttura documento
* Rimuovi compressione
* Non toccare la compressione

**Utilizzate Flate Per Codificare I Flussi Non Codificati**: Applica la compressione Flate a tutti i flussi non codificati.

**Elimina segnalibri** non validi: Rimuove i segnalibri che puntano alle pagine del documento che vengono eliminate.

**Elimina destinazioni** denominate senza riferimenti: Rimuove dall&#39;interno del documento PDF le destinazioni denominate alle quali non viene fatto riferimento internamente. Questa opzione non verifica la presenza di collegamenti da altri file PDF o siti Web.

**Ottimizzare Il PDF Per Una Visualizzazione** Web Rapida: Consente di riorganizzare un documento PDF per il download di una pagina alla volta (byte-serving) dai server Web.

**Nei Flussi Che Utilizzano La Codifica LZW, Utilizzate Invece** Flate: Applica la compressione Flate a tutti i flussi di contenuto e alle immagini che utilizzano la codifica LZW.

**Elimina collegamenti** non validi: Rimuove i collegamenti che consentono di passare a destinazioni non valide.

**Ottimizza contenuto** pagina: Converte tutti i caratteri di fine riga in spazi, migliorando la compressione Flate.

## Impostazioni di Microsoft Excel (solo Windows) {#microsoft-excel-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file Microsoft Excel. Per istruzioni su come accedere a queste opzioni, vedere [Creare o modificare le impostazioni dei tipi di file](#create-or-edit-file-type-settings).

**Prova OpenOffice Come Convertitore** di fallback: Quando questa opzione è selezionata e una conversione con Microsoft Excel non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, nel file di registro viene scritta un&#39;eccezione.

**Estensioni** nome file: Specifica le estensioni del nome file per i tipi di file, separati da virgole, che vengono accettate per questa applicazione. Il valore predefinito è `xls,xlsx`. Non includete un punto prima o uno spazio tra le estensioni.

**Crea file** conforme con PDF/A-1a: Forza l’utilizzo dell’impostazione PDF/A-1b:2005 RGB  Adobe PDF.

**Aggiungi Segnalibri A  Adobe PDF**: Converte i nomi dei fogli di lavoro di Excel in segnalibri. Per impostazione predefinita, questa opzione è selezionata.

**Adatta foglio di lavoro a una singola pagina**: Riduce le dimensioni del testo per adattarlo al foglio di lavoro su una singola pagina.

**Converti intera cartella di lavoro**: Converte tutti i fogli di lavoro nel file Excel. Se questa opzione non è selezionata, viene convertita solo la pagina corrente.

**Esegui macro automaticamente**: Esegue qualsiasi macro nel documento Excel (ad esempio una macro che inserisce l&#39;ora corrente) prima di convertire il documento.

**Converti informazioni** documento: Aggiunge proprietà del documento PDF basate sulle informazioni del documento nel file di origine. Sono incluse informazioni quali titolo del documento, autore, oggetto e parole chiave.

**Aggiungere Collegamenti A  Adobe PDF**: Converte i collegamenti ipertestuali nel file sorgente in collegamenti ipertestuali nel documento PDF.

**Allega File Di Origine A  Adobe PDF**: Quando questa opzione è selezionata, il foglio di calcolo Excel originale viene inserito come allegato nel documento PDF generato.

**Abilita Accessibilità E Reflow Con Tag  Adobe PDF**: Incorpora i tag all&#39;interno del documento PDF per abilitare l&#39;accessibilità e la ridisposizione.

**Elenco Di Componenti Aggiuntivi Di Excel Da Caricare**: Per impostazione predefinita (per motivi di sicurezza), quando un file Excel viene convertito in PDF non viene eseguito alcun componente aggiuntivo di Excel. Per consentire l&#39;esecuzione di alcuni componenti aggiuntivi di Excel durante la conversione, fornite un elenco separato da virgole dei nomi dei componenti aggiuntivi.

**Elenco Di Fogli Di Lavoro Da Convertire**: Quando questa casella è vuota, tutti i fogli di lavoro del foglio di calcolo Excel vengono inclusi nel PDF generato. Per convertire in modo selettivo un sottoinsieme di fogli di lavoro, specificare un elenco separato da virgole di nomi dei fogli di lavoro.

## Impostazioni di Microsoft PowerPoint (solo Windows) {#microsoft-powerpoint-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file Microsoft PowerPoint. Per istruzioni su come accedere a queste opzioni, vedere [Creare o modificare le impostazioni dei tipi di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Prova OpenOffice Come Convertitore]** di fallback: Quando questa opzione è selezionata e una conversione con Microsoft PowerPoint non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, nel file di registro viene scritta un&#39;eccezione.

**[!UICONTROL Estensioni]** nome file: Specifica le estensioni del nome file per i tipi di file, separati da virgole, che vengono accettate per questa applicazione. Il valore predefinito è ppt,pptx. Non includete un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni]** documento: Aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, società, categoria e commenti. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Aggiungi Segnalibri A  Adobe PDF]**: Converte i titoli di PowerPoint in segnalibri. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Allega File Di Origine A  Adobe PDF]**: Aggiunge il file sorgente al file PDF come allegato. Per impostazione predefinita questa opzione è deselezionata.

**[!UICONTROL Abilita Accessibilità E Reflow Con Tag  Adobe PDF]**: Incorpora i tag nel file PDF. Per impostazione predefinita questa opzione è deselezionata.

**[!UICONTROL Converti file multimediali in file multimediali]** PDF: Converte i file multimediali in file multimediali PDF, se possibile. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Converti note]** relatore: Converte le note dei relatori in PDF.

**[!UICONTROL Esegui macro automaticamente]**: Esegue qualsiasi macro nel documento PowerPoint (ad esempio una macro che inserisce l&#39;ora corrente) prima di convertire il documento.

**[!UICONTROL Layout PDF basato sulle impostazioni]** della stampante PowerPoint: Utilizza le impostazioni della stampante PowerPoint per il layout del documento PDF.

**[!UICONTROL Aggiungere Collegamenti A  Adobe PDF]**: Mantiene i collegamenti esistenti quando il file viene convertito. L&#39;aspetto dei collegamenti è generalmente invariato. I collegamenti possono essere creati solo se è selezionata anche l&#39;opzione Abilita accessibilità. Per impostazione predefinita questa opzione è deselezionata.

**[!UICONTROL Salva Transizioni Diapositive In  Adobe PDF]**: Converte le transizioni delle diapositive. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Salva Animazioni In  Adobe PDF]**: Salva le animazioni convertite nel file PDF.

**[!UICONTROL Converti diapositive nascoste in pagine]** PDF: Converte le diapositive nascoste.

**[!UICONTROL Crea file]** conforme con PDF/A-1a: Forza l’utilizzo dell’impostazione PDF/A-1b:2005 RGB  Adobe PDF. Alcune funzioni di PowerPoint non vengono convertite quando si crea un file PDF. Se una transizione PowerPoint non ha una transizione equivalente in  Acrobat, viene sostituita una transizione simile. Se più effetti di animazione si trovano nella stessa diapositiva, viene utilizzato un singolo effetto. Le transizioni di pagina e i plug-in vengono convertiti.

## Impostazioni Microsoft Project (solo Windows) {#microsoft-project-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file Microsoft Project. Per istruzioni su come accedere a queste opzioni, vedere [Creare o modificare le impostazioni dei tipi di file](#create-or-edit-file-type-settings).

1. **[!UICONTROL Estensioni nome file:]** specifica le estensioni del nome file per i tipi di file, separati da virgole, che vengono accettate per questa applicazione. Il valore predefinito è `mpp`. Non includete un punto prima o uno spazio tra le estensioni.

1. **[!UICONTROL Converti informazioni]** documento: Aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, società, categoria e commenti. Per impostazione predefinita, questa opzione è selezionata.
1. **[!UICONTROL Allega File Di Origine A  Adobe PDF]**: Aggiunge il file sorgente al file PDF come allegato.
1. **[!UICONTROL Crea file]** conforme con PDF/A-1a: Forza l’utilizzo dell’impostazione PDF/A-1b:2005 RGB  Adobe PDF.
1. **[!UICONTROL Esegui macro automaticamente]**: Esegue qualsiasi macro nel documento di Microsoft Project (ad esempio una macro che inserisce l&#39;ora corrente) prima di convertire il documento.

## Impostazioni di Microsoft Word (solo Windows) {#microsoft-word-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft Word. Per istruzioni su come accedere a queste opzioni, vedere [Creare o modificare le impostazioni dei tipi di file](#create-or-edit-file-type-settings).

**[!UICONTROL Prova OpenOffice Come Convertitore]** di fallback: Quando questa opzione è selezionata e una conversione con Microsoft Word non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, nel file di registro viene scritta un&#39;eccezione.

**[!UICONTROL Estensioni]** nome file: Specifica le estensioni del nome file per i tipi di file, separati da virgole, che vengono accettate per questa applicazione. Il valore predefinito è `doc,docx,rtf,txt`. Non includete un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni]** documento: Aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, società, categoria e commenti. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Aggiungi Segnalibri A  Adobe PDF]**: Converte le intestazioni in segnalibri. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Allega File Di Origine A  Adobe PDF]**: Aggiunge il file sorgente al file PDF come allegato.

**[!UICONTROL Converti Riferimenti E Sommario In Collegamenti]**: Converte tutti i riferimenti incrociati e le voci del sommario in collegamenti. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Abilita Accessibilità E Reflow Con Tag  Adobe PDF]**: Incorpora i tag nel file PDF. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Crea file]** conforme con PDF/A-1a: Se questa opzione è selezionata, forza l’utilizzo dell’impostazione PDF/A-1b:2005 RGB  Adobe PDF.

**[!UICONTROL Esegui macro automaticamente]**: Esegue qualsiasi macro nel documento Word (ad esempio una macro che inserisce l&#39;ora corrente) prima di convertire il documento.

**[!UICONTROL Mantieni markup documento in  Adobe PDF]**: Converte la marcatura nel documento Word in annotazioni nel file PDF.

**[!UICONTROL Aggiungere Collegamenti A  Adobe PDF]**: Converte i collegamenti ipertestuali nel file sorgente in collegamenti ipertestuali nel documento PDF.

**[!UICONTROL Converti Collegamenti]** Nota A Piè Di Pagina E Nota Di Chiusura: Crea collegamenti dalle note a piè di pagina e di chiusura alle note presenti nel documento PDF.

**[!UICONTROL Converti commenti visualizzati in note in  Adobe PDF]**: Converte i commenti nel documento Word in note di testo nel documento PDF.

**[!UICONTROL Abilita tag]** avanzati: Aggiunge tag avanzati per una migliore accessibilità.

**[!UICONTROL Converti tutti gli stili in segnalibri]**: Converte tutti gli stili del documento Word in segnalibri nel documento PDF.

**[!UICONTROL Stili Con Livelli]**: Specifica quali stili del documento Word vengono convertiti in segnalibri nel documento PDF. Specifica anche il livello dei segnalibri. Per utilizzare questa funzione, deselezionare l&#39;opzione **[!UICONTROL Converti tutti gli stili in segnalibri]** e specificare i nomi degli stili nel formato seguente:

**styleName1=level1[,styleName2=level2...]**

Se il nome di uno stile di Microsoft Word include una virgola (,) o un segno di uguale (=), anteporre i caratteri speciali al carattere di escape (&quot;\_). Ad esempio, specificare uno stile denominato &quot;Titolo, 1&quot; come Intestazione\, 1.

**Codifica di Acrobat PDFMaker:** specifica il tipo di codifica dei file di testo normale di input in Acrobat PDFMaker . Ad esempio, se utilizzate un file con codifica UTF-8, selezionate UTF-8 per ottenere risultati ottimali.

## Impostazioni di Microsoft Visio (solo Windows) {#visio}

**Converti informazioni** documento: Aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, società, categoria e commenti. Per impostazione predefinita, questa opzione è selezionata. Questa opzione è attivata per impostazione predefinita.

**Aggiungere Collegamenti A  Adobe PDF**: Mantiene tutti i collegamenti. Per impostazione predefinita, questa opzione è selezionata.

**Aggiungi Segnalibri A  Adobe PDF**: Converte le intestazioni in segnalibri. Per impostazione predefinita, questa opzione è selezionata.

**Allega File Di Origine A  Adobe PDF**: Aggiunge il file sorgente al file PDF come allegato.

**Appiattisci sempre i livelli in  Adobe PDF**: Appiattisce tutti i livelli di Visio.

**Converti tutte le pagine**: Converte tutte le pagine del file Visio.

**Aprite Il Pannello Livelli Quando Visualizzato In  Adobe Acrobat**: Se i livelli di Visio non sono appiattiti, apre una finestra in cui è possibile specificare i livelli che vengono conservati nel file PDF quando vengono aperti con  Acrobat. Per impostazione predefinita, questa opzione è selezionata.

**Crea file** conforme con PDF/A-1b: Impone l&#39;utilizzo dell&#39;impostazione Adobe PDF  PDF/A-1b:2005 (RGB).

**Converti Commenti In  Commenti** Adobe PDF: Converte le note di Visio in commenti PDF.

## Impostazioni di Microsoft Publisher (solo Windows) {#microsoft-publisher-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft Publisher. Per istruzioni su come accedere a queste opzioni, vedere [Creare o modificare le impostazioni dei tipi di file](#create-or-edit-file-type-settings).

**[!UICONTROL Estensioni]** nome file: Specifica le estensioni del nome file per i tipi di file, separati da virgole, che vengono accettate per questa applicazione. Il valore predefinito è `pub`. Non includete un punto prima o uno spazio tra le estensioni.

## Impostazioni AutoCAD (solo Windows) {#autocad-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file AutoCAD. Per istruzioni su come accedere a queste opzioni, vedere [Creare o modificare le impostazioni dei tipi di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Estensioni]** nome file: Specifica le estensioni del nome file per i tipi di file, separati da virgole, che vengono accettate per questa applicazione. Il valore predefinito è `dwg`. Non includete un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni]** documento: Aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, società, categoria e commenti. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Aggiungi Segnalibri A  Adobe PDF]**: Converte le intestazioni in segnalibri.

**[!UICONTROL Appiattisci sempre i livelli in  Adobe PDF]**: Appiattisce tutti i livelli AutoCAD.

**[!UICONTROL Apri Riquadro Livelli Visualizzato In  Adobe Acrobat]**: Mostra la struttura dei livelli quando il PDF viene aperto in  Acrobat.

**[!UICONTROL Converti tutti i layout]**: Include tutti i layout nel PDF.

**[!UICONTROL Converti spazio modello in 3D]**: Quando è selezionato, il layout dello spazio modello viene convertito in un&#39;annotazione 3D nel PDF.

**[!UICONTROL Aggiungere Collegamenti A  Adobe PDF]**: Se selezionato, mantiene tutti i collegamenti.

**[!UICONTROL Allega File Di Origine A  Adobe PDF]**: Aggiunge il file sorgente al file PDF come allegato.

**[!UICONTROL Crea file]** conforme con PDF/A-1b: Impone l&#39;utilizzo dell&#39;impostazione PDF/A-1b  Adobe PDF.

**[!UICONTROL Converti tutti i livelli]**: Per impostazione predefinita, PDF Generator converte in PDF solo il livello predefinito dei file AutoCAD anziché tutti i livelli contenuti nel file. Selezionate questa opzione per convertire tutti i livelli del file.

**[!UICONTROL Incorpora informazioni]** scala: Mantiene le informazioni sulla scala del disegno.

**[!UICONTROL Converti layout]** corrente: Include solo il layout corrente nel PDF.

**[!UICONTROL Elenco di layout AutoCAD da convertire]**: Un disegno AutoCAD può avere più layout. Se questa casella è vuota, tutti i layout del disegno AutoCAD vengono inclusi nel documento PDF generato. Per convertire in modo selettivo un sottoinsieme di layout, fornite un elenco separato da virgole di nomi di layout.

## Impostazioni OpenOffice {#openoffice-settings}

Queste opzioni determinano la modalità di conversione dei file OpenOffice. Per istruzioni su come accedere a queste opzioni, vedere [Creare o modificare le impostazioni dei tipi di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Provare PDFMaker Come Convertitore** di fallback: Quando questa opzione è selezionata e una conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando PDFMaker. Se la conversione con PDFMaker non riesce o raggiunge il limite di timeout specificato, nel file di registro viene scritta un&#39;eccezione.

**Estensioni** nome file: Specificate le estensioni di file per i tipi di file, separati da virgole, che vengono accettate per questa applicazione. Il valore predefinito è `odt,odp,ods,odg,odf,sxw,sxi,sxd`. Non includete un punto prima o uno spazio tra le estensioni.

**Intervallo**: Convertite tutte le pagine o specificate pagine particolari o un intervallo di pagine. Se un intervallo di pagine non è definito, tutte le pagine vengono convertite. Per esportare un intervallo di pagine, usate il formato 3-6. Per esportare pagine singole, usate il formato 7;9;11. È possibile esportare una combinazione di intervalli di pagine e singole pagine utilizzando un formato come 3-6;8;10;12.

**Orientamento** pagina: Solo per i file di testo normale, selezionare verticale o orizzontale per il documento PDF convertito.

**Immagini**: Configurare la modalità di conversione delle immagini. Le immagini EPS con anteprime incorporate vengono esportate solo come anteprime. Le immagini EPS senza anteprime incorporate vengono esportate come segnaposto vuoti. Con la compressione senza perdita di dati delle immagini, tutti i pixel vengono mantenuti. Con la compressione JPEG delle immagini e un livello di qualità elevato, vengono mantenuti quasi tutti i pixel. Con un livello di qualità basso, alcuni pixel si perdono e vengono introdotti artefatti, ma le dimensioni dei file sono ridotte.

**Generale**: Abilitare le opzioni per convertire un PDF con tag o per esportare le note del documento Writer e FormCalc, Imprimere effetti di transizione delle diapositive o pagine vuote nel PDF. Quando i tag vengono esportati, le dimensioni del file possono aumentare di grandi dimensioni. Alcuni tag esportati sono sommario, collegamenti ipertestuali e controlli.

È inoltre possibile specificare la modalità di invio dei moduli. Le opzioni sono XML, FDF, PDF o HTML. Questa impostazione sostituisce la proprietà URL del controllo impostata nel documento. Per il documento PDF è possibile selezionare una sola impostazione comune:

* PDF (invia l’intero documento)
* FDF (invia il contenuto del controllo)
* HTML
* XML

**PDF** con tag: Abilita la creazione di PDF con tag dai documenti OpenOffice. I PDF con tag contengono informazioni sulla struttura del contenuto del documento. Questo può essere utile quando si visualizza il documento su dispositivi con schermi diversi e quando si utilizza il software dell&#39;assistente vocale. Consente inoltre al software di accesso facilitato di eseguire varie operazioni utili con il documento PDF, ad esempio la lettura a voce alta del contenuto del documento PDF.

**Note** di esportazione: Converte le note presenti nei documenti OpenOffice in note nel documento PDF generato.

**Usa effetti** di transizione: Converte gli effetti di transizione della diapositiva nelle presentazioni OpenOffice in effetti di transizione PDF corrispondenti.

**Invia Forms In Formato**: Crea un modulo PDF che può essere compilato e stampato dall&#39;utente del documento PDF.

**Esporta automaticamente pagine** vuote inserite: Quando questa opzione è selezionata, nel documento PDF generato vengono inserite automaticamente pagine vuote. Questa funzione è utile se si stampa un documento PDF fronte/retro. Ad esempio, un libro può essere configurato in modo che la prima pagina del capitolo inizi sempre su una pagina dispari. Se il capitolo precedente termina su una pagina dispari, OpenOffice inserisce una pagina pari vuota. Questa opzione controlla se includere la pagina pari nel PDF generato.

## Altre impostazioni applicazione (solo Windows) {#other-applications-settings-windows-only}

Non è possibile modificare le impostazioni per altre applicazioni tramite la console di amministrazione; visualizzano le estensioni del nome file per i tipi di file supportati. Per istruzioni su come accedere a queste impostazioni, vedere [Creare o modificare le impostazioni dei tipi di file](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* PageMaker Adobe : `pmd, pm6, p65, pm`
*  Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Potrebbe essere necessario personalizzare il supporto per questi tipi di file. Per ulteriori informazioni, vedere &quot;Aggiunta del supporto per formati di file nativi aggiuntivi&quot; in [Programmazione con AEM moduli](https://www.adobe.com/go/learn_aemforms_programming_62).

Per informazioni sulla configurazione di una stampante di rete PDFG, vedere [Impostazione di una stampante di rete PDFG (solo Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
