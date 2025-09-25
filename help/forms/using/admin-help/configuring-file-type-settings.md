---
title: Configurare le impostazioni tipo di file
description: Scopri come configurare le impostazioni tipo di file. In PDF Generator, puoi configurare le impostazioni di applicazione per i tipi di file supportati per configurare le impostazioni tipo di file.
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
feature: PDF Generator
exl-id: 1a6640cc-22ef-41d5-a0c6-7a2c2dabcef1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '6195'
ht-degree: 100%

---

# Configurare le impostazioni tipo di file {#configuring-file-type-settings}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

In PDF Generator, puoi configurare le impostazioni di applicazione per i tipi di file supportati. In Windows, puoi configurare le impostazioni di applicazione per ogni tipo di file supportato. In UNIX e Linux, puoi configurare le impostazioni di applicazione per HTML-to-PDF e OpenOffice.

Nella pagina Impostazioni tipo di file, puoi eseguire le seguenti attività:

* [Creare o modificare un’impostazione tipo di file](#create-or-edit-file-type-settings)
* Specificare quali impostazioni tipo di file utilizzare per impostazione predefinita (consulta [Importazione ed esportazione dei file di configurazione di PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md))
* [Modificare le impostazioni predefinite](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)
* [Abilitare il supporto per PDF/A](/help/forms/using/admin-help/enable-pdf-a-support.md)
* [Eliminare un’impostazione di tipo file](/help/forms/using/admin-help/enable-pdf-a-support.md)

>[!NOTE]
>
>Le impostazioni del tipo di file non sono disponibili per i convertitori fallback come Acrobat per la conversione da HTML a PDF, Microsoft PowerPoint, Microsoft Word e Microsoft Excel.

## Creare o modificare le impostazioni del tipo di file {#create-or-edit-file-type-settings}

Crea o modifica un’impostazione del tipo di file per specificare il modo in cui l’applicazione gestisce la conversione dei tipi di file supportati. In Windows, puoi configurare le impostazioni di applicazione per ogni tipo di file supportato. In UNIX e Linux, puoi configurare le impostazioni di applicazione per HTML-to-PDF e OpenOffice.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Servizi]** > **[!UICONTROL PDF Generator]** > **[!UICONTROL Impostazioni tipo file]**.
1. Fai clic su Nuovo o sul nome di un’impostazione.
1. Nella casella Estensioni nome file digita le estensioni del nome file, separate da virgole, per i tipi di file accettati per l’applicazione. Non includere il punto prima o uno spazio tra le estensioni. Il valore predefinito è `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Facoltativo) Per utilizzare il riconoscimento ottico dei caratteri (OCR) del testo in grafiche o immagini, seleziona Usa OCR e imposta le seguenti opzioni:

**Lingua OCR principale:** la lingua che il motore OCR deve utilizzare per identificare i caratteri. L’impostazione predefinita è Inglese (US).

**Stile output PDF:** seleziona Immagine ricercabile per visualizzare un’immagine bitmap delle pagine in primo piano e il testo digitalizzato su un livello invisibile sottostante. L’aspetto della pagina non cambia, ma il testo diventa selezionabile e leggibile. Seleziona Testo e grafica formattati per ricreare la pagina originale utilizzando testo, font, immagini e altri elementi grafici riconosciuti. L’impostazione predefinita è Immagine ricercabile (Esatta).

**Sotto-campionamento immagini:** riduce il numero di pixel nelle immagini a colori, in scala di grigi e monocromatiche. Il sotto-campionamento delle immagini digitalizzate viene eseguito dopo il completamento dell’OCR. L’impostazione predefinita è Minore (600 dpi). Questa opzione non è disponibile se lo stile di output PDF è impostato su Immagine ricercabile (Esatta).

1. Compila le informazioni richieste nelle sezioni seguenti:

[Importazione ed esportazione dei file di configurazione di PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)

[Impostazioni di esportazione Adobe PDF (solo Windows)](#adobe-pdf-export-settings-windows-only)

[Impostazioni da HTML a PDF](#html-to-pdf-settings)

[Impostazioni di video Flash su PDF](#flash-videos-to-pdf-settings)

[Impostazioni da XPS a PDF](#xps-to-pdf-settings)

[Impostazioni di PDF Optimizer](/help/forms/using/admin-help/configuring-file-type-settings.md)

[Impostazioni di Microsoft Excel (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-excel-settings-windows-only)

[Impostazioni di Microsoft PowerPoint (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-powerpoint-settings-windows-only)

[Impostazioni progetto Microsoft (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-project-settings-windows-only)

[Impostazioni di Microsoft Word (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-word-settings-windows-only)

[Impostazioni di Microsoft Visio (solo Windows)](#visio)

[Impostazioni di Microsoft Publisher (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-publisher-settings-windows-only)

[Impostazioni AutoCAD (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#autocad-settings-windows-only)

[Impostazioni di OpenOffice](/help/forms/using/admin-help/configuring-file-type-settings.md#openoffice-settings)

[Impostazioni di altre applicazioni (solo Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#other-applications-settings-windows-only)

   Per passare a un’altra sezione, fai clic sul relativo collegamento nella pagina web oppure utilizza i pulsanti **[!UICONTROL Successivo]** o **[!UICONTROL Precedente]**.

1. Dopo aver completato tutte le sezioni, fai clic su **[!UICONTROL Salva]** o **[!UICONTROL Salva con nome]** e specifica un nome per l’impostazione

È possibile personalizzare il supporto per vari tipi di file. Consulta “[Aggiunta di supporto per formati aggiuntivi di file nativi](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)” in [Programmazione con AEM Forms](https://www.adobe.com/go/learn_lc_programming_11).

## Modificare le impostazioni predefinite {#change-the-default-settings}

Puoi modificare il valore predefinito per le impostazioni di Adobe PDF, le impostazioni di protezione e le impostazioni del tipo di file applicabili alle origini appena create. La modifica dei valori predefiniti non influisce sulle impostazioni delle origini esistenti.

1. In Console di amministrazione, fai clic su **[!UICONTROL Servizi > PDF Generator]**.
1. Nella pagina **[!UICONTROL Impostazioni Adobe PDF]**, **[!UICONTROL Impostazioni tipo file]** o **[!UICONTROL Impostazioni protezione]**, fai clic su **[!UICONTROL Configura impostazioni predefinite]**.
1. Seleziona le impostazioni predefinite preferite. Nella pagina Configura impostazioni predefinite sono disponibili una o più delle seguenti opzioni:

   **[!UICONTROL Impostazione Adobe PDF]**: il valore predefinito originale è Standard (Acrobat 6).

   **[!UICONTROL Impostazioni protezione]**: il valore predefinito originale è Nessuna protezione (Acrobat 5).

   **[!UICONTROL Impostazioni tipo file]**: il valore predefinito originale è Standard.

1. Fai clic su **[!UICONTROL Salva]**.

## Eliminare un’impostazione di tipo file {#delete-a-file-type-setting}

È possibile eliminare un’impostazione del tipo file non più utilizzata.

1. In Console di amministrazione, fai clic su **[!UICONTROL Servizi > PDF Generator> Impostazioni di tipo file]**.
1. Seleziona la casella di controllo accanto all’impostazione da eliminare. È possibile selezionare più origini. Le impostazioni che non hanno accanto una casella di controllo sono sempre incluse in PDF Generator e non possono essere eliminate.
1. Fai clic su **[!UICONTROL Elimina]** e nella pagina Conferma eliminazione fai clic su **[!UICONTROL Elimina]**.

## Impostazioni da immagine a PDF {#image-to-pdf-settings}

Le seguenti opzioni determinano la modalità di conversione dei file di immagine in PDF. Per istruzioni sull’accesso a queste impostazioni, consulta [Creare o modificare le impostazioni del tipo file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Estensioni dei nomi di file:** elenco separato da virgole delle estensioni dei nomi di file che è possibile convertire.

**Prova il convertitore di fallback:** PDF Generator può utilizzare Java™ o Acrobat per convertire i file immagine in PDF. Quando selezioni questa opzione e una conversione non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando il metodo alternativo. Se il metodo alternativo non riesce o raggiunge il limite di timeout specificato, nel file di registro viene scritta un’eccezione.

>[!NOTE]
>
>I file JPEG 2000 possono essere convertiti solo con Acrobat.

**Usa OCR:** specifica se applicare OCR (riconoscimento ottico dei caratteri) al PDF. Il software OCR consente di cercare, correggere e copiare il testo nel PDF.

***nota **: la funzionalità PDF OCR (PDF ricercabile) è supportata solo in Microsoft Windows.*

**Lingua OCR principale:** specifica la lingua che il motore OCR deve utilizzare per identificare i caratteri.

**Stile output PDF:** determina il tipo di PDF da produrre. Tutti i formati consentono di applicare il riconoscimento OCR e font e pagina alle immagini di testo e di convertirle in testo normale.

**Immagine ricercabile:** assicura che il testo sia ricercabile e selezionabile. Questa opzione mantiene l’immagine originale, la disegna in base alle esigenze e posiziona sopra di essa un livello di testo invisibile. L’opzione di Sotto-campionamento immagini determina se l’immagine viene ricampionata e in quale misura.

**Immagine ricercabile (esatta):** assicura che il testo sia ricercabile e selezionabile. Questa opzione mantiene l’immagine originale e posiziona sopra di essa un livello di testo invisibile. Consigliato per le situazioni che richiedono la massima fedeltà all’immagine originale.

**ClearScan:** sintetizza un nuovo font di tipo 3 che si avvicina all’originale e mantiene lo sfondo della pagina utilizzando una copia a bassa risoluzione.

**Sotto-campionamento immagini:** riduce il numero di pixel nelle immagini a colori, in scala di grigio e monocromatiche dopo il completamento dell’OCR. Scegli il livello di sotto-campionamento da applicare. Le opzioni con un numero più alto eseguono un downsampling inferiore, producendo PDF con una risoluzione più elevata.

## Impostazioni di esportazione Adobe PDF (solo Windows) {#adobe-pdf-export-settings-windows-only}

L’impostazione Tipo di file di esportazione nella sezione Impostazioni di esportazione Adobe PDF viene utilizzata per convertire un file PDF in un altro formato. Il valore predefinito è HTML 4.01 con fogli di stile CSS 1.0 (*.htm, *.html).

Per istruzioni sull’accesso a questa impostazione, consulta [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Impostazioni da HTML a PDF {#html-to-pdf-settings}

Le seguenti opzioni determinano la modalità di conversione dei file HTML in PDF. Per istruzioni sull’accesso a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Prova convertitore fallback:** PDF Generator può utilizzare Java™ o Acrobat per convertire i file HTML in PDF. Quando selezioni questa opzione e una conversione non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando il metodo alternativo. Se il metodo alternativo non riesce o raggiunge il limite di timeout specificato, nel file di registro viene scritta un’eccezione.

**Codifica predefinita:** imposta la codifica di input del testo del file da un menu di sistemi operativi e alfabeti. Utilizza la selezione mostrata nell’opzione Codifica predefinita solo se il file di origine HTML non specifica un tipo di codifica.

**Forza codifica selezionata:** ignora la codifica specificata nel file di origine HTML e utilizza la selezione visualizzata nell’opzione Codifica predefinita.

### Impostazioni spider {#spidering-settings}

*Spider* ricerca nelle pagine web i collegamenti ad altre pagine web. Quando viene rilevato un collegamento a un’altra pagina web, la pagina di destinazione viene recuperata e inclusa nel documento PDF generato. Abilita queste opzioni per impostare il numero di livelli da recuperare e convertire in PDF:

**Ottieni solo X livelli:** esegue spider e converte le pagine fino a una profondità del livello specificato dall’URL della pagina base. Un valore pari a 1 converte solo l’URL specificato.

**Ottieni intero sito:** converte l’intero sito, a partire dall’URL specificato.

**Resta sullo stesso percorso:** tutti i collegamenti che puntano a pagine che non si trovano nello stesso percorso relativo dell’URL di base non vengono convertiti durante spider.

**Resta sullo stesso server:** i collegamenti che puntano a pagine su server diversi non vengono convertiti durante spider. Vengono convertiti solo i collegamenti che puntano allo stesso server dell’URL specificato.

### Impostazioni di conversione pagina {#page-conversion-settings}

Abilita queste opzioni per specificare la modalità di conversione delle pagine HTML. In base alle dimensioni della pagina, i valori di larghezza, altezza e margine vengono modificati di conseguenza.

**Dimensioni della pagina:** scegli l’opzione personalizzata e specifica la larghezza e l’altezza oppure seleziona le dimensioni predefinite.

**Orientamento:** seleziona verticale od orizzontale per il documento PDF convertito.

**Margini:** specifica i margini (superiore, inferiore, sinistro e destro) nel documento PDF generato.

**Aggiungi segnalibri a PDF:** aggiunge segnalibri al documento PDF.

**Abilita PDF con tag:** incorpora i tag nel documento PDF.

**Imposta impostazioni visualizzazione iniziale:** ti consente di configurare le opzioni documento, finestra e interfaccia utente. Queste impostazioni determinano la modalità di visualizzazione iniziale del contenuto.

### Opzioni documento {#document-options}

Abilita queste opzioni per specificare come visualizzare il contenuto, come visualizzare le pagine nel documento PDF e come specificare il livello di ingrandimento:

**Mostra:** seleziona i riquadri da aprire in Acrobat all’apertura del documento PDF.

**Layout pagina:** seleziona il tipo di layout pagina per il documento PDF.

**Ingrandimento:** scegli l’ingrandimento predefinito per la visualizzazione iniziale del documento PDF oppure seleziona un valore personalizzato. La scelta di un’impostazione predefinita indica che viene utilizzato l’ingrandimento predefinito di Acrobat.

**Apri a numero pagina:** specifica il numero di pagina a cui si apre il PDF.

### Opzioni finestra {#window-options}

Abilita queste opzioni per specificare le dimensioni e la visualizzazione della finestra.

**Ridimensiona finestra alla pagina iniziale:** ridimensiona la finestra di Acrobat alle dimensioni della pagina iniziale.

**Centra finestra sullo schermo:** apre la finestra al centro dello schermo.

**Apri in modalità a schermo inrero:** apre la finestra in modalità a schermo intero.

**Mostra:** visualizza il titolo o il nome del file del documento nella finestra.

### Opzioni interfaccia utente {#user-interface-options}

Abilita queste opzioni per specificare l’aspetto della finestra:

**Nascondi barra dei menu:** nasconde la barra dei menu nel documento PDF.

**Nascondi barre degli strumenti:** nasconde le barre degli strumenti nel documento PDF.

**Nascondi controlli finestra:** nasconde i controlli finestra nel documento PDF.

## Impostazioni di video Flash su PDF {#flash-videos-to-pdf-settings}

PDF Generator supporta la possibilità di inviare un video per Adobe Flash (file SWF o FLV) e di creare un file PDF con un video per Adobe Flash incorporato. Questa conversione non richiede l’installazione di Adobe Flash Player sul server Forms. Per istruzioni sull’accesso a questa opzione, consulta [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Estensioni dei nomi di file:** elenco separato da virgole delle estensioni dei nomi di file che è possibile convertire.

## Impostazioni da XPS a PDF {#xps-to-pdf-settings}

XPS (XML Paper Specification) viene utilizzato in una macchina di stampa Windows. Questo è un formato Microsoft e può essere creato da qualsiasi applicazione di Microsoft Office. AEM Forms consente di convertire i file XPS in PDF.

**Estensioni del nome file:** elenco separato da virgole di tutte le estensioni del nome file XPS che è possibile convertire. Attualmente c’è un solo formato: .xps.

## Impostazioni di PDF optimizer {#pdf-optimizer-settings}

PDF Generator supporta la possibilità di ridurre le dimensioni dei file PDF. L’utilizzo di tutte queste impostazioni o solo di alcune dipende dal modo in cui intendi utilizzare i file e dalle proprietà essenziali necessarie. Nella maggior parte dei casi, le impostazioni predefinite sono appropriate per la massima efficienza: consente di risparmiare spazio rimuovendo i font incorporati, comprimendo le immagini e rimuovendo dai file gli elementi che non sono più necessari.

>[!NOTE]
>
>L’ottimizzazione di un documento con firma digitale rimuove e invalida le firme digitali.

Per istruzioni sull’accesso a questa impostazione, consulta [Creare o modificare le impostazioni del tipo file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Versione PDF di destinazione:** specifica la versione di Acrobat compatibile con il PDF.

### Font {#fonts}

1. Seleziona **Font.**
1. Seleziona una delle opzioni seguenti:

   **Non incorporare tutti i font:** non incorpora tutti i font incorporati.

   **Non annullare l’incorporamento di font:** non annulla l’incorporamento di font.

   **Non incorporare alcuni font:** non incorpora solo i font specificati. Per specificare i font che non desideri incorporare, effettua i passaggi successivi.

   * Se necessario, seleziona una directory diversa per i font dal menu a discesa **Origini font**. Questo menu a discesa elenca le directory dei font specificate in **Home > Impostazioni > Sistema core > Configurazioni core**.
   * Seleziona uno o più font dall’elenco **Font disponibili** e fai clic su **Aggiungi**. Questi font vengono aggiunti all’elenco **Font da non incorporare**.
   * Se desideri non incorporare alcuni font che non esistono nel server Forms, immetti i nomi di tali font nella casella **Aggiungi font da non incorporare**. Fai clic su **Aggiungi**.

   >[!NOTE]
   >
   >*Per non incorporare alcuni font i cui sottoinsiemi sono incorporati nel documento, anteponi al nome del font il segno +. Ad esempio, “+Helvetica”.*

1. Se desideri incorporare solo i sottoinsiemi in uso dei font incorporati, seleziona **Crea sottoinsieme di tutti i font incorporati**.

   >[!NOTE]
   >
   >*Se utilizzi questa opzione in combinazione con **Non incorporare alcuni font**, i font nell’elenco **Aggiungi font da non incorporare**sono comunque del tutto non incorporati.*

   >[!NOTE]
   >
   >*La creazione di un sottoinsieme di font è la tecnica di incorporamento di una sola parte di un carattere. Un sottoinsieme di font contiene solo i caratteri utilizzati nel documento.*

### Trasparenza {#transparency}

Se il documento PDF include grafica che contiene trasparenza, puoi utilizzare le impostazioni di PDF Optimizer per appiattire la trasparenza e ridurre le dimensioni del file.

>[!NOTE]
>
>Se selezioni Acrobat 4.0 e versioni successive come versione di destinazione del PDF, tutti gli oggetti trasparenti vengono appiattiti. Per altre versioni di destinazione del PDF, la trasparenza è supportata e puoi configurarne le impostazioni.

Seleziona **Trasparenza** per configurare le impostazioni di trasparenza durante l’ottimizzazione dei documenti PDF.

**Livello di trasparenza** specifica la quantità di informazioni vettoriali che verranno mantenute. Impostazioni più elevate mantengono più oggetti vettoriali, mentre impostazioni più basse ne rasterizzano un maggior numero; le impostazioni intermedie mantengono aree semplici in forma vettoriale e rasterizzano quelle complesse. Seleziona l’impostazione più bassa per rasterizzare tutta la grafica.

>[!NOTE]
>
>La quantità di rasterizzazione dipende dalla complessità della pagina e dai tipi di oggetti sovrapposti.

**Grafica e testo** risoluzione con cui vengono rasterizzati tutti gli oggetti, inclusi immagini, grafica vettoriale, testo e sfumature. I valori supportati sono da 1 pixel per pollice (ppi) a 9600 ppi.

>[!NOTE]
>
>La risoluzione grafica e testo deve essere in genere impostata su 600-1200 ppi per fornire una rasterizzazione di alta qualità, in particolare sui caratteri serif e con dimensione in punti ridotta.

**Sfumatura e trame** la risoluzione con cui vengono rasterizzate la sfumatura e le trame. I valori supportati sono da 1 ppi a 1200 ppi.

>[!NOTE]
>
>La risoluzione sfumatura e trama deve essere generalmente impostata su 150-300 ppi perché la qualità delle sfumature, delle ombre esterne e dei contorni sfocati non migliora con risoluzioni più elevate, ma il tempo di stampa e le dimensioni del file aumentano.

**Converti tutto il testo in contorni** converte tutti gli oggetti di tipo (tipo di punto, tipo di area e tipo di percorso) in contorni e ignora tutte le informazioni sui glifi di tipo nelle pagine contenenti trasparenza. Questa opzione garantisce che la larghezza del testo rimanga coerente durante la conversione. L’attivazione di questa opzione provocherà un leggero aumento di spessore nei font di piccole dimensioni se visualizzati in Acrobat o stampati su stampanti desktop a bassa risoluzione. Non influisce sulla qualità del tipo stampato su stampanti o fotounità ad alta risoluzione.

**Converti tutte le tracce in contorni** converte tutte le tracce in semplici percorsi con riempimento nelle pagine contenenti trasparenza. Questa opzione garantisce che la larghezza delle tracce rimanga costante durante l’appiattimento. L’attivazione di questa opzione determina un leggero aumento di spessore delle tracce sottili e può compromettere le prestazioni di appiattimento.

**Ritaglia aree complesse** assicura che i limiti tra grafica vettoriale e grafica rasterizzata siano compresi nei percorsi degli oggetti. Questa opzione riduce gli artefatti di unione risultanti quando fanno parte di un

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Alcuni driver di stampa elaborano la grafica raster e la grafica vettoriale in modo diverso, talvolta con conseguente unione dei colori. Puoi ridurre al minimo i problemi di unione disabilitando alcune impostazioni di gestione dei colori specifiche per i driver di stampa. Queste impostazioni variano a seconda della stampante; per ulteriori informazioni, consulta la documentazione fornita con la stampante.

Mantieni sovrastampa: fonde il colore della grafica trasparente con il colore di sfondo per creare un effetto di sovrastampa.

Nella tabella seguente sono illustrati i tipi di stampanti più comuni e la relativa risoluzione misurata in dpi, la rigatura predefinita dello schermo misurata in linee per pollice (lpi) e una risoluzione di ricampionamento per le immagini misurata in pixel per pollice (ppi). Se ad esempio stampi su una stampante laser a 600 dpi, immetti 170 per la risoluzione con cui ricampionare le immagini.

**Immagini** seleziona Immagini per specificare le opzioni di compressione e ricampionamento per le immagini a colori, in scala di grigi e monocromatiche. Puoi sperimentare queste opzioni per trovare un giusto equilibrio tra le dimensioni del file e la qualità dell’immagine.L’impostazione della risoluzione per le immagini a colori e in scala di grigi deve essere da 1,5 a 2 volte la rigatura della retinatura a linee in corrispondenza della quale verrà stampato il file. La risoluzione per le immagini monocromatiche deve essere la stessa del dispositivo di output, ma il salvataggio di un’immagine monocromatica con una risoluzione superiore a 1500 dpi aumenta le dimensioni del file senza migliorare in modo significativo la qualità dell’immagine. Le immagini che verranno ingrandite, ad esempio le mappe, potrebbero richiedere risoluzioni più elevate.

>[!NOTE]
>
>Il ricampionamento delle immagini monocromatiche può produrre risultati di visualizzazione imprevisti, ad esempio la mancata visualizzazione delle immagini. In questo caso, disattiva il ricampionamento e converti nuovamente il file. Questo problema si verifica con maggiore probabilità con il sottocampionamento e con minore probabilità con il downsampling bicubico.

<table>
 <tbody>
  <tr>
   <th><p><strong>Risoluzione della stampante</strong></p> </th>
   <th><p><strong>Retinatura a linee predefinita</strong></p> </th>
   <th><p><strong>Risoluzione dell’immagine</strong></p> </th>
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

#### Eliminare oggetti {#discard-objects}

* Seleziona **Elimina oggetti** per specificare gli oggetti da rimuovere dal PDF e ottimizzare le linee curve nei disegni CAD.
* **Elimina tutte le azioni di invio, importazione e reimpostazione dei moduli**: disabilita tutte le azioni correlate all’invio o all’importazione dei dati dei moduli e reimposta i campi dei moduli. Questa opzione mantiene gli oggetti modulo a cui sono collegate le azioni.
* **Elimina tutte le azioni di JavaScript**: rimuove dal PDF tutte le azioni che utilizzano JavaScript.
* **Elimina miniature pagina incorporate**: rimuove le miniature di pagina incorporate. Questa opzione è utile per i documenti di grandi dimensioni, che possono richiedere molto tempo per disegnare le miniature di pagina dopo che hai fatto clic sul pulsante Pagine.
* **Converti linee smussate in curve**: riduce il numero di punti di controllo utilizzati per creare curve nei disegni CAD, con conseguente riduzione dei file PDF e maggiore rapidità di rendering sullo schermo.
* **Elimina impostazioni di stampa incorporate**: rimuove dal documento le impostazioni di stampa incorporate, ad esempio il ridimensionamento delle pagine e la modalità fronte-retro.
* **Elimina segnalibri**: rimuove tutti i segnalibri dal documento.
* **Appiattisci campi modulo**: rende inutilizzabili i campi modulo senza modificarne l’aspetto. I dati del modulo vengono uniti alla pagina per diventare contenuto della pagina.
* **Elimina tutte le immagini alternative**: rimuove tutte le versioni di un’immagine ad eccezione della versione destinata alla visualizzazione sullo schermo. Alcuni PDF includono più versioni della stessa immagine per scopi diversi, ad esempio la visualizzazione su schermo a bassa risoluzione e la stampa ad alta risoluzione.
* **Elimina i tag del documento**: rimuove i tag dal documento, eliminando anche le funzionalità di accessibilità e ridisposizione del testo
* **Rileva e unisci frammenti di immagini**: cerca immagini o maschere frammentate in porzioni sottili e tenta di unire le porzioni in un’unica immagine o maschera.
* **Elimina indice di ricerca incorporato**: rimuove gli indici di ricerca incorporati, riducendo le dimensioni del file.

#### Elimina dati utente {#discard-user-data}

Seleziona **Elimina dati utente** per rimuovere le informazioni personali che non desideri distribuire o condividere con altri utenti.

* **Elimina tutti i commenti, i moduli e i file multimediali**: rimuove tutti i commenti, i moduli, i campi dei moduli e i file multimediali dal PDF.
* **Elimina tutti i dati oggetto**: rimuove tutti gli oggetti dal PDF.
* **Elimina riferimenti incrociati esterni**: rimuove i collegamenti ad altri documenti. I collegamenti che fanno saltare ad altre posizioni all’interno del PDF non vengono rimossi.
* **Elimina contenuto dei livelli nascosti e appiattisci i livelli visibili**: riduce le dimensioni del file. Il documento ottimizzato è simile al PDF originale, ma non contiene informazioni sui livelli.
* **Elimina le informazioni del documento e i metadadi**: rimuove le informazioni dal dizionario delle informazioni del documento e tutti i flussi di metadati (utilizza il comando Salva con nome per ripristinare i flussi di metadati in una copia del PDF).
* **Elimina gli allegati dei file**: rimuove tutti gli allegati, inclusi quelli aggiunti al PDF come commenti (PDF Optimizer non ottimizza i file allegati).
* **Elimina i dati privati di altre applicazioni**: elimina da un documento PDF le informazioni utili solo per l’applicazione che ha creato il documento. Questa impostazione non influisce sulla funzionalità del PDF, ma riduce le dimensioni del file.

### Pulisci {#clean-up}

Seleziona **Pulisci** per rimuovere gli elementi non necessari dal documento.
Questi elementi includono quelli obsoleti o non necessari per l’utilizzo previsto del documento. La rimozione di alcuni elementi può compromettere gravemente la funzionalità del PDF. Per impostazione predefinita, vengono selezionati solo gli elementi che non influiscono sulla funzionalità. In caso di dubbi sulle implicazioni relative alla rimozione di altre opzioni, utilizza le selezioni predefinite.

**Compressione**

Seleziona una delle seguenti opzioni di compressione Flate dal menu a discesa:

* Comprimi intero file
* Comprimi struttura documento
* Rimuovi compressione
* Lascia intatta la compressione

**Utilizza Flate per codificare i flussi non codificati**: applica la compressione Flate a tutti i flussi non codificati.

**Elimina segnalibri non validi**: rimuove i segnalibri che puntano alle pagine eliminate del documento.

**Elimina destinazioni denominate senza riferimento**: rimuove dal documento PDF le destinazioni denominate a cui non si fa riferimento internamente. Questa opzione non verifica la presenza di collegamenti da altri file PDF o siti web.

**Ottimizza PDF per la visualizzazione web veloce**: ristruttura un documento PDF per consentire il download pagina per pagina (byte serving) dai server web.

**Per i flussi codificati con LZW, utilizza invece Flate**: applica la compressione Flate a tutti i flussi di contenuto e alle immagini che utilizzano la codifica LZW.

**Elimina collegamenti non validi**: rimuove i collegamenti che passano a destinazioni non valide.

**Ottimizza contenuto pagina**: converte tutti i caratteri di fine riga in spazi, migliorando così la compressione Flate.

## Impostazioni di Microsoft Excel (solo Windows) {#microsoft-excel-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft Excel. Per istruzioni sull’accesso a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

**Prova OpenOffice come convertitore di fallback**: quando questa opzione è selezionata e una conversione con Microsoft Excel non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, nel file di log viene riportata un’eccezione.

**Estensioni del nome file**: specifica le estensioni dei nomi dei file per i tipi di file, separate da virgole, che sono accettate per questa applicazione. Il valore predefinito è `xls,xlsx`. Non includere un punto prima o uno spazio tra le estensioni.

**Crea file conforme a PDF/A-1a**: impone l’utilizzo dell’impostazione di Adobe PDF PDF/A-1b:2005 RGB.

**Aggiungi segnalibri ad Adobe PDF**: converte i nomi dei fogli di lavoro di Excel in segnalibri. Questa opzione è selezionata per impostazione predefinita.

**Adatta foglio di lavoro a una singola pagina**: riduce le dimensioni del testo per adattarlo al foglio di lavoro in una singola pagina.

**Converti intera cartella di lavoro**: converte tutti i fogli di lavoro nel file di Excel. Se questa opzione non è selezionata, viene convertita solo la pagina corrente.

**Esegui automaticamente macro**: esegue le macro nel documento di Excel, ad esempio una macro che inserisce l’ora corrente, prima di convertire il documento.

**Converti informazioni documento**: aggiunge al documento PDF le proprietà in base alle informazioni presenti nel file di origine. Ciò include informazioni quali titolo del documento, autore, oggetto e parole chiave.

**Aggiungi collegamenti ad Adobe PDF**: converte i collegamenti ipertestuali nel file di origine in collegamenti ipertestuali nel documento PDF.

**Allega file di origine ad Adobe PDF**: quando questa opzione è selezionata, il foglio di calcolo Excel originale viene inserito come allegato nel documento PDF generato.

**Abilita accessibilità e ridisposizione con tag Adobe PDF**: incorpora i tag nel documento PDF per abilitare l’accessibilità e la ridisposizione.

**Elenco dei componenti aggiuntivi di Excel da caricare**: per impostazione predefinita (per motivi di sicurezza), nessun componente aggiuntivo di Excel viene eseguito quando il file viene convertito in PDF. Per consentire l’esecuzione di alcuni componenti aggiuntivi di Excel durante la conversione, fornisci un elenco separato da virgole dei nomi dei componenti aggiuntivi.

**Elenco dei fogli di lavoro da convertire**: quando questa casella è vuota, tutti i fogli di lavoro nel foglio di calcolo di Excel vengono inclusi nel PDF generato. Per convertire in modo selettivo un sottoinsieme dei fogli di lavoro, fornisci un elenco separato da virgole di nomi dei fogli di lavoro.

## Impostazioni di Microsoft PowerPoint (solo Windows) {#microsoft-powerpoint-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft PowerPoint. Per istruzioni sull’accesso a queste opzioni, consulta [Creare o modificare le impostazioni del tipo file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Prova OpenOffice come convertitore di fallback]**: quando questa opzione è selezionata e una conversione con Microsoft PowerPoint non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, nel file di log viene riportata un’eccezione.

**[!UICONTROL Estensioni del nome file]**: specifica le estensioni del nome file per i tipi file, separati da virgole, accettati per l’applicazione. Il valore predefinito è ppt, pptx. Non includere un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni documento]**: aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, gestore, società, categoria e commenti. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Aggiungi segnalibri ad Adobe PDF]**: converte i titoli di PowerPoint in segnalibri. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Allega file di origine ad Adobe PDF]**: aggiunge il file di origine al file PDF come allegato. Questa opzione è deselezionata per impostazione predefinita.

**[!UICONTROL Abilita accessibilità e ridisposizione con tag Adobe PDF]**: incorpora i tag nel file PDF. Questa opzione è deselezionata per impostazione predefinita.

**[!UICONTROL Converti contenuti multimediali in contenuti multimediali PDF]**: se possibile, converte contenuti multimediali in contenuti multimediali PDF. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Converti note relatore]**: converte le note relatore in PDF.

**[!UICONTROL Esegui automaticamente macro]**: esegue le macro nel documento di PowerPoint, ad esempio una macro che inserisce l’ora corrente, prima di convertire il documento.

**[!UICONTROL Layout PDF basato sulle impostazioni della stampante di PowerPoint]**: utilizza le impostazioni della stampante di PowerPoint per creare il layout del documento PDF.

**[!UICONTROL Aggiungi collegamenti ad Adobe PDF]**: mantiene i collegamenti esistenti quando il file viene convertito. L’aspetto dei collegamenti è generalmente invariato. I collegamenti possono essere creati solo se è selezionata anche l’opzione Abilita accessibilità. Questa opzione è deselezionata per impostazione predefinita.

**[!UICONTROL Salva transizioni diapositive in Adobe PDF]**: converte le transizioni tra diapositive. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Salva animazioni in Adobe PDF]**: salva le animazioni convertite nel file PDF.

**[!UICONTROL Converti diapositive nascoste in pagine PDF]**: converte le diapositive nascoste.

**[!UICONTROL Crea file conforme a PDF/A-1a]**: impone l’utilizzo dell’impostazione di Adobe PDF PDF/A-1b:2005 RGB. Alcune funzionalità di PowerPoint non vengono convertite quando generi un file PDF. Se una transizione di PowerPoint non ha un’equivalente in Acrobat, viene sostituita una transizione simile. Se più effetti di animazione si trovano nella stessa diapositiva, viene utilizzato un unico effetto. Le transizioni di pagina e i punti elenco fly-in vengono convertiti.

## Impostazioni progetto Microsoft (solo Windows) {#microsoft-project-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di progetto di Microsoft. Per istruzioni sull’accesso a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

1. **[!UICONTROL Estensioni nome file:]** specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l’applicazione. L’impostazione predefinita è `mpp`. Non includere un punto prima o uno spazio tra le estensioni.

1. **[!UICONTROL Converti informazioni documento]**: aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, azienda, categoria e commenti. Questa opzione è selezionata per impostazione predefinita.
1. **[!UICONTROL Allega file di origine ad Adobe PDF]**: aggiunge il file di origine al file PDF come allegato.
1. **[!UICONTROL Crea file conforme a PDF/A-1a]**: forza l’utilizzo dell’impostazione PDF/A-1b:2005 RGB Adobe PDF.
1. **[!UICONTROL Esegui automaticamente macro]**: esegue le macro nel documento del progetto Microsoft (ad esempio una macro che inserisce l’ora corrente) prima di convertire il documento.

## Impostazioni di Microsoft Word (solo Windows) {#microsoft-word-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft Word. Per istruzioni sull’accesso a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

**[!UICONTROL Prova OpenOffice come convertitore fallback]**: quando selezioni questa opzione e una conversione con Microsoft Word non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, nel file di log viene riportata un’eccezione.

**[!UICONTROL Estensioni nome file]**: specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l’applicazione. L’impostazione predefinita è `doc,docx,rtf,txt`. Non includere un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni documento]**: aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, azienda, categoria e commenti. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Aggiungi segnalibri ad Adobe PDF]**: converte le intestazioni in segnalibri. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Allega file di origine ad Adobe PDF]**: aggiunge il file di origine al file PDF come allegato.

**[!UICONTROL Converti riferimenti incrociati e sommario in collegamenti]**: converte tutti i riferimenti incrociati e le voci del sommario in collegamenti. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Abilita accessibilità e ridisposizione con tag Adobe PDF]**: incorpora i tag nel file PDF. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Crea file conforme a PDF/A-1a]**: se selezionata, forza l’utilizzo dell’impostazione PDF/A-1b:2005 RGB Adobe PDF.

**[!UICONTROL Esegui automaticamente macro]**: esegue tutte le macro nel documento Word (ad esempio una macro che inserisce l’ora corrente) prima di convertire il documento.

**[!UICONTROL Mantieni markup documento in Adobe PDF]**: converte il markup nel documento Word in annotazioni nel file PDF.

**[!UICONTROL Aggiungi collegamenti ad Adobe PDF]**: converte i collegamenti ipertestuali nel file di origine in collegamenti ipertestuali nel documento PDF.

**[!UICONTROL Converti collegamenti note a piè di pagina e note di chiusura]**: crea collegamenti dalle citazioni nelle note a piè di pagina e note di chiusura alle note nel documento PDF.

**[!UICONTROL Converti commenti visualizzati in note in Adobe PDF]**: converte i commenti nel documento Word in note di testo nel documento PDF.

**[!UICONTROL Abilita assegnazione tag avanzati]**: aggiunge tag avanzati per migliorare l’accessibilità.

**[!UICONTROL Converti tutti gli stili in segnalibri]**: converte tutti gli stili nel documento Word in segnalibri nel documento PDF.

**[!UICONTROL Converti stili specificati in segnalibri]**: converte gli stili definiti nel campo **[!UICONTROL Stili con livelli]** in segnalibri nel documento PDF.

**[!UICONTROL Stili con livelli]**: specifica quali stili nel documento Word vengono convertiti in segnalibri nel documento PDF. Specifica inoltre il livello dei segnalibri. Per utilizzare questa funzione, deseleziona l’opzione **[!UICONTROL Converti tutti gli stili in segnalibri]** e specifica i nomi degli stili nel formato seguente:

**styleName1=level1[,styleName2=level2...]**

Se un nome di stile di Microsoft Word include una virgola (,) o un segno di uguale (=), anteponi ai caratteri speciali il carattere di escape (&quot;\_). Ad esempio, specifica uno stile denominato “Intestazione, 1” come Intestazione\, 1.

**Codifica Acrobat PDFMaker:** specifica il tipo di codifica dei file di testo non formattati di input per Acrobat PDFMaker. Ad esempio, se utilizzi un file codificato UTF-8, seleziona UTF-8 per ottenere risultati ottimali.

## Impostazioni di Microsoft Visio (solo Windows) {#visio}

**Converti informazioni documento**: aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, azienda, categoria e commenti. Questa opzione è selezionata per impostazione predefinita. Questa opzione è abilitata per impostazione predefinita.

**Aggiungi collegamenti ad Adobe PDF**: mantiene tutti i collegamenti. Questa opzione è selezionata per impostazione predefinita.

**Aggiungi segnalibri ad Adobe PDF**: converte le intestazioni in segnalibri. Questa opzione è selezionata per impostazione predefinita.

**Allega file di origine ad Adobe PDF**: aggiunge il file di origine al file PDF come allegato.

**Livelli sempre appiattiti in Adobe PDF**: appiattisce tutti i livelli di Visio.

**Converti tutte le pagine**: converte tutte le pagine del file Visio.

**Apri riquadro livelli quando visualizzato in Adobe Acrobat**: se i livelli di Visio non vengono appiattiti, apre una finestra in cui puoi specificare i livelli che vengono conservati nel file PDF quando vengono aperti con Acrobat. Questa opzione è selezionata per impostazione predefinita.

**Crea file conforme a PDF/A-1b**: forza l’utilizzo dell’impostazione di Adobe PDF PDF/A-1b:2005 (RGB).

**Converti commenti in commenti Adobe PDF**: converte le note di Visio in commenti PDF.

## Impostazioni di Microsoft Publisher (solo Windows) {#microsoft-publisher-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft Publisher. Per istruzioni sull’accesso a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

**[!UICONTROL Estensioni nome file]**: specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l’applicazione. L’impostazione predefinita è `pub`. Non includere un punto prima o uno spazio tra le estensioni.

## Impostazioni AutoCAD (solo Windows) {#autocad-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file AutoCAD. Per istruzioni sull’accesso a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Estensioni nome file]**: specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l’applicazione. L’impostazione predefinita è `dwg`. Non includere un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni documento]**: aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, azienda, categoria e commenti. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Aggiungi segnalibri ad Adobe PDF]**: converte le intestazioni in segnalibri.

**[!UICONTROL Appiattisci sempre livelli in Adobe PDF]**: appiattisce tutti i livelli di AutoCAD.

**[!UICONTROL Apri riquadro livelli quando visualizzato in Adobe Acrobat]**: mostra la struttura dei livelli quando il PDF viene aperto in Acrobat.

**[!UICONTROL Converti tutti i layout]**: include tutti i layout nel PDF.

**[!UICONTROL Converti spazio modello in 3D]**: se selezionata, il layout dello spazio modello viene convertito in un’annotazione 3D nel PDF.

**[!UICONTROL Aggiungi collegamenti ad Adobe PDF]**: se selezionata, mantiene tutti i collegamenti.

**[!UICONTROL Allega file di origine ad Adobe PDF]**: aggiunge il file di origine al file PDF come allegato.

**[!UICONTROL Crea file conforme a PDF/A-1b]**: forza l’utilizzo dell’impostazione PDF/A-1b Adobe PDF.

**[!UICONTROL Converti tutti i livelli]**: per impostazione predefinita, PDF Generator converte solo il livello predefinito dei file AutoCAD in PDF anziché tutti i livelli all’interno del file. Seleziona questa opzione per convertire tutti i livelli del file.

**[!UICONTROL Incorpora informazioni ridimensionamento]**: mantiene le informazioni sul ridimensionamento del disegno.

**[!UICONTROL Converti layout corrente]**: include solo il layout corrente nel PDF.

**[!UICONTROL Elenco dei layout AutoCAD da convertire]**: un disegno AutoCAD può avere più layout. Se questa casella è vuota, tutti i layout del disegno AutoCAD vengono inclusi nel documento PDF generato. Per convertire selettivamente un sottoinsieme di layout, fornisci un elenco separato da virgole di nomi di layout.

## Impostazioni di OpenOffice {#openoffice-settings}

Queste opzioni determinano la modalità di conversione dei file di OpenOffice. Per istruzioni sull’accesso a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Prova PDFMaker come convertitore fallback**: quando selezioni questa opzione e una conversione con OpenOffice non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando PDFMaker. Se la conversione tramite PDFMaker non riesce o raggiunge il limite di timeout specificato, nel file di registro viene scritta un’eccezione.

**Estensioni nome file**: specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l’applicazione. L’impostazione predefinita è `odt,odp,ods,odg,odf,sxw,sxi,sxd`. Non includere un punto prima o uno spazio tra le estensioni.

**Intervallo**: converti tutte le pagine o specifica pagine particolari o un intervallo di pagine. Se non definisci un intervallo di pagine, vengono convertite tutte le pagine. Per esportare un intervallo di pagine, utilizza il formato 3-6. Per esportare pagine singole, utilizza il formato 7;9;11. Puoi esportare una combinazione di intervalli di pagine e pagine singole utilizzando un formato come 3-6;8;10;12.

**Orientamento pagina**: solo per i file di testo normale, seleziona Verticale o Orizzontale per il documento PDF convertito.

**Immagini**: configura la modalità di conversione delle immagini. Le immagini EPS con anteprime incorporate vengono esportate solo come anteprime. Le immagini EPS senza anteprime incorporate vengono esportate come segnaposto vuoti. Con la compressione delle immagini senza perdita di dati, tutti i pixel vengono mantenuti. Con la compressione JPEG delle immagini e un livello di qualità elevato, vengono mantenuti quasi tutti i pixel. Con un livello di qualità basso, alcuni pixel si perdono e vengono introdotti artefatti, ma le dimensioni dei file si riducono.

**Generale**: abilita le opzioni per convertire un PDF con tag o esportare le note dei documenti Writer e FormCalc, gli effetti di transizione delle diapositive Impress o le pagine vuote in PDF. Quando si esportano i tag, la dimensione del file può aumentare in modo significativo. Alcuni tag esportati sono sommari, collegamenti ipertestuali e controlli.

Puoi inoltre specificare la modalità di invio dei moduli. Le opzioni sono XML, FDF, PDF o HTML. Questa impostazione sovrascrive la proprietà URL del controllo impostata nel documento. Per il documento PDF è possibile selezionare una sola impostazione comune:

* PDF (invia l’intero documento)
* FDF (invia il contenuto del controllo)
* HTML
* XML

**PDF con tag**: consente la creazione di PDF con tag dai documenti di OpenOffice. Il PDF con tag contiene informazioni sulla struttura del contenuto del documento. Questo può essere utile quando il documento viene visualizzato su dispositivi con schermi diversi e quando si utilizza un software di assistente vocale. Consente inoltre al software di accessibilità di eseguire varie operazioni utili con il documento PDF, ad esempio la lettura ad alta voce del contenuto.

**Esporta note**: converte le note dei documenti OpenOffice in note nel documento PDF generato.

**Usa effetti di transizione**: converte gli effetti di transizione delle diapositive nelle presentazioni di OpenOffice negli effetti di transizione dei PDF corrispondenti.

**Invia in formato modulo**: crea un modulo PDF che può essere compilato e stampato dall’utente del documento PDF.

**Esporta automaticamente pagine vuote inserite**: quando questa opzione è selezionata, le pagine vuote inserite automaticamente vengono incluse nel documento PDF generato. Questa opzione è utile se si stampa un documento PDF su due lati. Ad esempio, un libro può essere configurato in modo che la prima pagina del capitolo inizi sempre su una pagina con numero dispari. Se il capitolo precedente termina su una pagina con numero dispari, OpenOffice inserisce una pagina vuota con numero pari. Questa opzione controlla se includere la pagina con numero pari nel PDF generato.

## Altre impostazioni dell’applicazione (solo Windows) {#other-applications-settings-windows-only}

Non puoi modificare le impostazioni per altre applicazioni tramite la console di amministrazione, poiché visualizzano le estensioni dei nomi di file per i tipi di file supportati. Per istruzioni sull’accesso a queste impostazioni, consulta [Creare o modificare le impostazioni del tipo di file](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* Adobe PageMaker: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Potresti dover personalizzare il supporto per questi tipi di file. Per ulteriori informazioni, consulta “Aggiunta di supporto per formati di file nativi aggiuntivi” in [Programmazione con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_62).

Per informazioni sulla configurazione di una stampante di rete PDFG, consulta [Configurazione di una stampante di rete PDFG (solo Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
