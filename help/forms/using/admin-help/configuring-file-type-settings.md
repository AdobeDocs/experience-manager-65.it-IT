---
title: Configurazione delle impostazioni del tipo di file
seo-title: Configuring file type settings
description: Scopri come configurare le impostazioni del tipo di file.
seo-description: Learn how to configure file type settings.
uuid: ab037659-c6ff-4de9-9417-f5a6fc8122cb
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ab19b248-8931-4cf6-b6a5-fb7b067c4a49
feature: PDF Generator
exl-id: 1a6640cc-22ef-41d5-a0c6-7a2c2dabcef1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6158'
ht-degree: 2%

---

# Configurazione delle impostazioni del tipo di file {#configuring-file-type-settings}

In PDF Generator è possibile impostare le impostazioni dell&#39;applicazione per i tipi di file supportati. In Windows è possibile impostare le impostazioni dell&#39;applicazione per ogni tipo di file supportato. Su UNIX e Linux, è possibile impostare le impostazioni dell&#39;applicazione per HTML-to-PDF e OpenOffice.

Nella pagina Impostazioni tipo di file è possibile eseguire le operazioni seguenti:

* [Creare o modificare un’impostazione Tipo di file](#create-or-edit-file-type-settings)
* Specificare le impostazioni del tipo di file da utilizzare per impostazione predefinita (vedere [Importazione ed esportazione di file di configurazione di PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md))
* [Modificare le impostazioni predefinite](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)
* [Abilita supporto PDF/A](/help/forms/using/admin-help/enable-pdf-a-support.md)
* [Eliminare un’impostazione di tipo file](/help/forms/using/admin-help/enable-pdf-a-support.md)

>[!NOTE]
>
>Le impostazioni del tipo di file non sono disponibili per i convertitori di fallback, come Acrobat per la conversione da HTML a PDF, Microsoft PowerPoint, Microsoft Word e Microsoft Excel.

## Creare o modificare le impostazioni del tipo di file {#create-or-edit-file-type-settings}

Crea o modifica un&#39;impostazione di tipo file per specificare come l&#39;applicazione gestisce la conversione dei tipi di file supportati. In Windows è possibile impostare le impostazioni dell&#39;applicazione per ogni tipo di file supportato. Su UNIX e Linux, è possibile impostare le impostazioni dell&#39;applicazione per HTML-to-PDF e OpenOffice.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Servizi]** > **[!UICONTROL Generatore PDF]** > **[!UICONTROL Impostazioni tipo di file]**.
1. Fare clic su Nuovo o sul nome di un&#39;impostazione.
1. Nella casella Estensioni nome file digitare le estensioni del nome file, separate da virgole, per i tipi di file accettati per questa applicazione. Non includere il periodo precedente o uno spazio tra le estensioni. Il valore predefinito è `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Facoltativo) Per utilizzare il riconoscimento ottico del codice (OCR) del testo in immagini o immagini, selezionare Usa OCR e impostare le seguenti opzioni:

**Lingua OCR principale:** La lingua utilizzata dal motore OCR per identificare i caratteri. Il valore predefinito è Inglese (US).

**Stile di output di PDF:** Selezionare Immagine ricercabile per avere un&#39;immagine bitmap delle pagine in primo piano e il testo scansionato su un livello invisibile sotto. L’aspetto della pagina non cambia, ma il testo diventa selezionabile e leggibile. Selezionare Testo formattato e grafica per ricostruire la pagina originale utilizzando testo, font, immagini e altri elementi grafici riconosciuti. Il valore predefinito è Immagine ricercabile (Esatto).

**Scarica le immagini:** Diminuisce il numero di pixel nelle immagini a colori, in scala di grigi e monocromatiche. Il sottocampionamento delle immagini scansionate viene eseguito dopo il completamento dell&#39;OCR. Il valore predefinito è Più basso (600 dpi). Questa opzione non è disponibile se lo stile di output di PDF è impostato su Immagine ricercabile (Esatto).

1. Compila le informazioni richieste nelle sezioni seguenti:

[Importazione ed esportazione di file di configurazione di PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)

[Impostazioni di esportazione Adobe PDF (solo Windows)](#adobe-pdf-export-settings-windows-only)

[Impostazioni HTML-to-PDF](#html-to-pdf-settings)

[Flash video alle impostazioni di PDF](#flash-videos-to-pdf-settings)

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

   Per passare a un’altra sezione, fai clic sul relativo collegamento sulla pagina web o utilizza il **[!UICONTROL Successivo]** o **[!UICONTROL Precedente]** pulsanti.

1. Dopo aver completato tutte le sezioni, fai clic su **[!UICONTROL Salva]** o **[!UICONTROL Salva con nome]** e fornisci un nome per l&#39;impostazione.

È possibile personalizzare il supporto per vari tipi di file. (Vedi &quot; [Aggiunta del supporto per formati di file nativi aggiuntivi](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot; [Programmazione con moduli AEM](https://www.adobe.com/go/learn_lc_programming_11).)

## Modificare le impostazioni predefinite {#change-the-default-settings}

È possibile modificare il valore predefinito per le impostazioni di Adobe PDF, le impostazioni di protezione e le impostazioni del tipo di file che si applicano alle origini appena create. La modifica delle impostazioni predefinite non influisce sulle impostazioni delle origini esistenti.

1. In Console di amministrazione, fai clic su **[!UICONTROL Servizi > PDF Generator]**.
1. Sulla **[!UICONTROL Impostazioni di Adobe PDF]**, **[!UICONTROL Impostazioni tipo di file]** oppure **[!UICONTROL Impostazioni di protezione]** pagina, fai clic su **[!UICONTROL Imposta impostazioni predefinite]**.
1. Seleziona le impostazioni predefinite preferite. Nella pagina Imposta impostazioni predefinite sono disponibili una o più delle seguenti impostazioni:

   **[!UICONTROL Impostazione Adobe PDF]**: Il valore predefinito originale è Standard (Acrobat 6).

   **[!UICONTROL Impostazioni di protezione]**: Il valore predefinito originale è Nessuna protezione (Acrobat 5).

   **[!UICONTROL Impostazioni tipo di file]**: Il valore predefinito originale è Standard.

1. Fai clic su **[!UICONTROL Salva]**.

## Eliminare un’impostazione di tipo file {#delete-a-file-type-setting}

È possibile eliminare un’impostazione di tipo file non più utilizzata.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Servizi > PDF Generator> Impostazioni dei tipi di file]**.
1. Seleziona la casella di controllo accanto all’impostazione da eliminare. È possibile selezionare più sorgenti. Le impostazioni prive di una casella di controllo accanto a esse sono sempre incluse in PDF Generator e non possono essere eliminate.
1. Fai clic su **[!UICONTROL Elimina]** e, nella pagina Elimina conferma, fai clic su **[!UICONTROL Elimina]**.

## Impostazioni di PDF {#image-to-pdf-settings}

Le opzioni seguenti determinano la modalità di conversione dei file immagine in PDF. Per istruzioni su come accedere a queste impostazioni, consulta [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Estensioni nome file:** Elenco delle estensioni del nome file che possono essere convertite separate da virgole.

**Prova Fallback Converter:** PDF Generator può utilizzare Java™ o Acrobat per convertire i file immagine in PDF. Quando questa opzione è selezionata e una conversione non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando il metodo alternativo. Se il metodo alternativo non riesce o raggiunge il limite di timeout specificato, viene scritta un&#39;eccezione nel file di registro.

>[!NOTE]
>
>I file di JPEG 2000 possono essere convertiti solo con Acrobat.

**Usa OCR:** Specifica se applicare l&#39;OCR (riconoscimento ottico dei caratteri) al PDF. Il software OCR consente di cercare, correggere e copiare il testo in PDF.

***nota **: La funzione OCR PDF (searchable PDF) è supportata solo su Microsoft Windows.*

**Lingua OCR principale:** Specifica la lingua che il motore OCR deve utilizzare per identificare i caratteri.

**Stile di output di PDF:** Determina il tipo di PDF da produrre. Tutti i formati applicano l&#39;OCR e il riconoscimento del font e della pagina alle immagini di testo e le convertono in testo normale.

**Immagine ricercabile:** Assicurati che il testo sia ricercabile e selezionabile. Questa opzione mantiene l&#39;immagine originale, la desktop in base alle esigenze e posiziona sopra di essa un livello di testo invisibile. L’opzione Downsample Images determina se l’immagine viene sottoposta a ricampionatura verso il basso e in che misura.

**Immagine ricercabile (Esatto):** Assicurati che il testo sia ricercabile e selezionabile. Questa opzione mantiene l’immagine originale e posiziona sopra di essa un livello di testo invisibile. Consigliato per i casi che richiedono la massima fedeltà all’immagine originale.

**ClearScan:** Sintetizza un nuovo font Type 3 che avvicina strettamente l&#39;originale e conserva lo sfondo della pagina utilizzando una copia a bassa risoluzione.

**Scarica le immagini:** Riduce il numero di pixel nelle immagini a colori, in scala di grigi e monocromatiche dopo il completamento dell&#39;OCR. Scegliere il grado di downsampling da applicare. Le opzioni numerate più elevate consentono di eseguire meno il downsampling, che produce PDF a risoluzione più elevata.

## Impostazioni di esportazione Adobe PDF (solo Windows) {#adobe-pdf-export-settings-windows-only}

L’impostazione Export File Type (Tipo file di esportazione) nella sezione delle impostazioni di esportazione di Adobe PDF viene utilizzata per convertire un file PDF in un altro formato. Il valore predefinito è HTML 4.01 con fogli di stile CSS 1.0 (*.htm, *.html).

Per istruzioni su come accedere a questa impostazione, vedi [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Impostazioni HTML-to-PDF {#html-to-pdf-settings}

Le opzioni seguenti determinano la modalità di conversione dei file HTML in PDF. Per istruzioni su come accedere a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Prova Fallback Converter:** PDF Generator può utilizzare Java™ o Acrobat per convertire i file HTML in PDF. Quando questa opzione è selezionata e una conversione non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando il metodo alternativo. Se il metodo alternativo non riesce o raggiunge il limite di timeout specificato, viene scritta un&#39;eccezione nel file di registro.

**Codifica predefinita:** Imposta la codifica di input del testo del file da un menu di sistemi operativi e alfabeti. Utilizza la selezione mostrata nell’opzione Codifica predefinita solo se il file di origine di HTML non specifica un tipo di codifica.

**Forza codifica selezionata:** Ignora le codifiche specificate nel file di origine di HTML e utilizza la selezione mostrata nell’opzione Codifica predefinita.

### Impostazioni ragnatela {#spidering-settings}

*Spiaggia* esegue la scansione di pagine web per individuare i collegamenti ad altre pagine web. Quando si incontra un collegamento a un’altra pagina web, la pagina di destinazione viene recuperata e inclusa nel documento PDF generato. Abilita queste opzioni per impostare il numero di livelli da recuperare e convertire in PDF:

**Ottieni Solo Livelli X:** Raggruppa e converte le pagine fino a una profondità del livello specificato dall’URL della pagina di base. Il valore 1 converte solo l’URL fornito.

**Ottieni l&#39;intero sito:** Converte l’intero sito, a partire dall’URL fornito.

**Sempre sullo stesso percorso:** Eventuali collegamenti che puntano a pagine che non si trovano sullo stesso percorso relativo dell’URL di base non vengono convertiti durante il ragionamento.

**Sempre sullo stesso server:** Eventuali collegamenti che puntano a pagine su server diversi non vengono convertiti durante il spider. Vengono convertiti solo i collegamenti che puntano allo stesso server dell’URL specificato.

### Impostazioni di conversione della pagina {#page-conversion-settings}

Abilitare queste opzioni per specificare la modalità di conversione delle pagine HTML. In base alle dimensioni della pagina, i valori di larghezza, altezza e margine si regolano di conseguenza.

**Dimensioni pagina:** Scegli l’opzione personalizzata e specifica la larghezza e l’altezza, oppure seleziona dimensioni predefinite.

**Orientamento:** Selezionare verticale o orizzontale per il documento PDF convertito.

**Margini:** Specifica i margini (superiore, inferiore, sinistro e destro) nel documento PDF generato.

**Aggiungi Segnalibri A PDF:** Aggiunge segnalibri al documento PDF.

**Abilita PDF con tag:** Incorpora i tag nel documento PDF.

**Imposta le impostazioni della vista iniziale:** Consente di configurare Opzioni documento, Opzioni finestra e Opzioni interfaccia utente. Queste impostazioni determinano la modalità di visualizzazione iniziale del contenuto.

### Opzioni documento {#document-options}

Abilitare queste opzioni per specificare come visualizzare il contenuto, come visualizzare le pagine nel documento PDF e come specificare il livello di ingrandimento:

**Mostra:** Selezionare i riquadri da aprire in Acrobat all’apertura del documento PDF.

**Layout della pagina:** Selezionare il tipo di layout di pagina per il documento PDF.

**Ingrandimento:** Scegliere l’ingrandimento predefinito per la visualizzazione iniziale del documento PDF o selezionare un valore personalizzato. La scelta di un’impostazione predefinita indica che verrà utilizzata l’ingrandimento predefinito di Acrobat.

**Apri al numero di pagina:** Specifica il numero di pagina a cui si apre il PDF.

### Opzioni finestra {#window-options}

Abilitare queste opzioni per specificare le dimensioni e la visualizzazione della finestra.

**Ridimensiona finestra alla pagina iniziale:** Ridimensiona la finestra Acrobat alle dimensioni della pagina iniziale.

**Finestra centrale sullo schermo:** Apre la finestra al centro dello schermo.

**Apri In Modalità A Schermo Intero:** Apre la finestra in modalità a tutto schermo.

**Mostra:** Visualizza il titolo o il nome del documento nella finestra.

### Opzioni interfaccia utente {#user-interface-options}

Abilita queste opzioni per specificare l’aspetto della finestra:

**Nascondi barra dei menu:** Nasconde la barra dei menu nel documento PDF.

**Nascondi barre degli strumenti:** Nasconde le barre degli strumenti nel documento PDF.

**Nascondi controlli finestra:** Nasconde i controlli della finestra nel documento PDF.

## Flash video alle impostazioni di PDF {#flash-videos-to-pdf-settings}

PDF Generator supporta la possibilità di inviare un video per Adobe Flash (file SWF o FLV) e di creare un file PDF con un video, ad Adobe incorporato al suo interno. Questa conversione non richiede l’installazione di un Flash Player Adobe nel server dei moduli. Per istruzioni su come accedere a questa opzione, consulta [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Estensioni nome file:** Elenco delle estensioni del nome file che possono essere convertite separate da virgole.

## Impostazioni da XPS a PDF {#xps-to-pdf-settings}

XML Paper Specification (XPS) viene utilizzato nella macchina di stampa di Windows. Si tratta di un formato Microsoft e può essere creato da qualsiasi applicazione Microsoft Office. I moduli AEM consentono di convertire file XPS PDF.

**Estensioni nome file:** Elenco separato da virgole di tutte le estensioni del nome file XPS che possono essere convertite. Attualmente esiste un formato: xps.

## Impostazioni di PDF Optimizer {#pdf-optimizer-settings}

PDF Generator supporta la possibilità di ridurre le dimensioni dei file PDF. Se si utilizzano tutte queste impostazioni o solo alcune dipende da come si intende utilizzare i file e dalle proprietà essenziali che un file deve avere. Nella maggior parte dei casi, le impostazioni predefinite sono appropriate per la massima efficienza: risparmiare spazio rimuovendo i font incorporati, comprimendo le immagini e rimuovendo gli elementi dai file che non sono più necessari.

>[!NOTE]
>
>L’ottimizzazione di un documento con firma digitale rimuove e invalida le firme digitali.

Per istruzioni su come accedere a questa impostazione, vedi [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Versione di Target PDF:** Specifica la versione di Acrobat con cui PDF è compatibile.

### Font {#fonts}

1. Seleziona **Font.**
1. Selezionare una delle seguenti opzioni:

   **Separa tutti i font:** Sincorpora tutti i font incorporati.

   **Non incorporare alcun font:** Non incorpora font.

   **Separa alcuni font:** Sincorpora solo i font specificati. Segui questi passaggi per specificare i font da rimuovere:

   * Se necessario, seleziona una directory di font diversa dal **Origine font** menu a discesa. Questo menu a discesa elenca le directory dei font specificate in **Home > Impostazioni > Sistema di base > Configurazioni di base**.
   * Seleziona uno o più font dal **Font disponibili** elenco e fai clic su **Aggiungi**. Questi font vengono aggiunti al **Font da rimuovere** elenco.
   * Se si desidera rimuovere alcuni font non esistenti nel server dei moduli, immettere i nomi di tali font nel **Aggiungi font da rimuovere** scatola. Fate clic su **Aggiungi**.

   >[!NOTE]
   >
   >*Se si desidera rimuovere alcuni font i cui sottoinsiemi sono incorporati nel documento, assegnare al nome del font il prefisso +. Ad esempio, &quot;+Helvetica&quot;.*

1. Se si desidera incorporare solo i sottoinsiemi in uso dei font incorporati, selezionare **Sottoimposta tutti i font incorporati**.

   >[!NOTE]
   >
   >*Se utilizzi questa opzione in combinazione con **Sincorporare alcuni font**, i font nel **Aggiungi font da rimuovere**elenco non incorporato.*

   >[!NOTE]
   >
   >*Il sottoinsieme di font è la tecnica utilizzata per incorporare solo una parte di un font. Un sottoinsieme di font contiene solo i caratteri utilizzati nel documento.*

### Trasparenza {#transparency}

Se il documento PDF include immagini che contengono trasparenza, è possibile utilizzare le impostazioni di PDF Optimizer per appiattire la trasparenza e ridurre le dimensioni del file.

>[!NOTE]
>
>Se Acrobat 4.0 e versioni successive è selezionato come versione di Target PDF, tutti gli oggetti trasparenti vengono appiattiti. Per altre versioni di Target PDF, la trasparenza è supportata e puoi configurare le impostazioni di trasparenza.

Seleziona **Trasparenza** per configurare le impostazioni di trasparenza durante l’ottimizzazione dei documenti PDF.

**Livello di trasparenza** Specifica la quantità di informazioni vettoriali che verranno mantenute. Le impostazioni più elevate conservano più oggetti vettoriali, mentre le impostazioni più basse rasterizzano più oggetti vettoriali; le impostazioni intermedie conservano le aree semplici in forma vettoriale e ne rasterizzano quelle complesse. Seleziona l&#39;impostazione più bassa per rasterizzare tutta l&#39;immagine.

>[!NOTE]
>
>La quantità di rasterizzazione che si verifica dipende dalla complessità della pagina e dai tipi di oggetti sovrapposti.

**Grafica e testo a linee** Risoluzione a cui vengono rasterizzati tutti gli oggetti, incluse immagini, immagini vettoriali, testo e sfumature. I valori supportati sono da 1 pixel per pollice (ppi) a 9600 ppi.

>[!NOTE]
>
>La risoluzione dell&#39;arte e del testo della linea dovrebbe essere generalmente impostata a 600-1200 ppi per fornire una rasterizzazione di alta qualità, soprattutto su serif o di piccole dimensioni punto.

**Sfumatura e sfumature** Risoluzione a cui sfumatura e trame sono rasterizzate. I valori supportati sono da 1 ppi a 1200 ppi.

>[!NOTE]
>
>La risoluzione della sfumatura e della mesh dovrebbe essere generalmente impostata su 150-300 ppi perché la qualità dei gradienti, delle ombre e delle piume non migliora con risoluzioni più elevate, ma il tempo di stampa e la dimensione del file aumentano.

**Converti tutto il testo in contorni** Converte tutti gli oggetti di tipo (tipo di punto, tipo di area e tipo di percorso) in contorni ed elimina tutte le informazioni di glifo di tipo sulle pagine contenenti trasparenza. Questa opzione assicura che la larghezza del testo rimanga uniforme durante l’appiattimento. L’abilitazione di questa opzione fa sì che i font piccoli appaiano leggermente più spessi quando vengono visualizzati in Acrobat o stampati su stampanti desktop a bassa risoluzione. Non influisce sulla qualità del tipo stampato su stampanti o fotounità ad alta risoluzione.

**Converti tutti i tratti in contorni** Converte tutti i tratti in semplici percorsi riempiti nelle pagine contenenti trasparenza. Questa opzione assicura che la larghezza dei tratti rimanga uniforme durante l&#39;appiattimento. L’abilitazione di questa opzione fa sì che i tratti sottili appaiano leggermente più spessi e possano peggiorare le prestazioni di appiattimento.

**Regioni complesse delle clip** Assicura che i limiti tra le immagini vettoriali e le immagini rasterizzate rientrino lungo i percorsi degli oggetti. Questa opzione riduce gli artefatti di unione che si verificano quando parte di un og

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Alcuni driver di stampa elaborano le immagini raster e vettoriali in modo diverso, a volte con conseguente unione dei colori. È possibile ridurre al minimo i problemi di unione disattivando alcune impostazioni di gestione del colore specifiche per i driver di stampa. Queste impostazioni variano a seconda della stampante, per ulteriori informazioni, consultare la documentazione fornita con la stampante.

Mantieni sovrastampa: Per creare un effetto di sovrastampa, fonde il colore dell&#39;immagine trasparente con il colore di sfondo.

La tabella seguente mostra i tipi più comuni di stampanti e la loro risoluzione misurata in dpi, la loro regola dello schermo predefinita misurata in linee per pollice (lpi) e una risoluzione di ricampionamento per le immagini misurate in pixel per pollice (ppi). Ad esempio, se si stampa su una stampante laser a 600 dpi, immettere 170 per la risoluzione a cui campionare le immagini.

**Immagini** Selezionare Immagini per specificare le opzioni di compressione e ricampionamento per le immagini a colori, in scala di grigi e monocromatiche. È possibile sperimentare queste opzioni per trovare un equilibrio appropriato tra le dimensioni del file e la qualità dell&#39;immagine.L&#39;impostazione di risoluzione per le immagini a colori e in scala di grigi deve essere da 1,5 a 2 volte la regola dello schermo a linee in cui il file verrà stampato. La risoluzione per le immagini monocromatiche dovrebbe essere la stessa del dispositivo di output, ma tieni presente che il salvataggio di un&#39;immagine monocromatica a una risoluzione superiore a 1500 dpi aumenta le dimensioni del file senza migliorare sensibilmente la qualità dell&#39;immagine. Le immagini che verranno ingrandite, come le mappe, potrebbero richiedere risoluzioni più elevate.

>[!NOTE]
>
>Il ricampionamento delle immagini monocromatiche può produrre risultati di visualizzazione imprevisti, ad esempio nessuna visualizzazione delle immagini. In questo caso, disattivare il ricampionamento e convertire di nuovo il file. Questo problema si verifica con maggiore probabilità con il sottocampionamento e con minore probabilità con il sottocampionamento bicubico.

<table>
 <tbody>
  <tr>
   <th><p><strong>Risoluzione della stampante</strong></p> </th>
   <th><p><strong>Schermata a linee predefinita</strong></p> </th>
   <th><p><strong>Risoluzione dell'immagine</strong></p> </th>
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

#### Elimina oggetti {#discard-objects}

* Seleziona **Elimina oggetti** specificare gli oggetti da rimuovere dal PDF e ottimizzare le linee curve nei disegni CAD.
* **Elimina Tutte Le Azioni Di Invio, Importazione E Reimpostazione Del Modulo**: Disattiva tutte le azioni relative all’invio o all’importazione dei dati del modulo e ripristina i campi del modulo. Questa opzione mantiene gli oggetti modulo a cui sono collegate le azioni.
* **Elimina tutte le azioni JavaScript**: Rimuove da PDF tutte le azioni che utilizzano JavaScript.
* **Elimina miniature di pagina incorporate**: Rimuove le miniature di pagina incorporate. Questa opzione è utile per i documenti di grandi dimensioni, che possono richiedere molto tempo per disegnare le miniature di pagina dopo aver fatto clic sul pulsante Pagine.
* **Converti linee smussate in curve**: Riduce il numero di punti di controllo utilizzati per creare curve nei disegni CAD, il che si traduce in file PDF più piccoli e in un rendering sullo schermo più veloce.
* **Elimina impostazioni di stampa incorporate**: Rimuove dal documento le impostazioni di stampa incorporate, ad esempio il ridimensionamento della pagina e la modalità fronte/retro.
* **Elimina segnalibri**: Rimuove tutti i segnalibri dal documento.
* **Campi modulo appiattiti**: Rende i campi modulo inutilizzabili senza modifiche al loro aspetto. I dati modulo vengono uniti alla pagina per diventare contenuto della pagina.
* **Elimina tutte le immagini alternative**: Rimuove tutte le versioni di un’immagine, ad eccezione della versione destinata alla visualizzazione sullo schermo. Alcuni PDF includono più versioni della stessa immagine per scopi diversi, ad esempio visualizzazione a schermo a bassa risoluzione e stampa ad alta risoluzione.
* **Elimina tag documento**: Rimuove i tag dal documento, rimuovendo anche le funzionalità di accesso facilitato e riflusso del testo.
* **Rileva E Unisci Frammenti Immagine**: Cerca immagini o maschere frammentate in fette sottili e cerca di unire le fette in un&#39;unica immagine o maschera.
* **Elimina indice di ricerca incorporato**: Rimuove gli indici di ricerca incorporati, riducendo le dimensioni del file.

#### Elimina dati utente {#discard-user-data}

Seleziona **Elimina dati utente** rimuovere le informazioni personali che non si desidera distribuire o condividere con altri utenti.

* **Elimina Tutti I Commenti, Forms E Multimedia**: Rimuove tutti i commenti, i moduli, i campi modulo e gli elementi multimediali da PDF.
* **Elimina tutti i dati oggetto**: Rimuove tutti gli oggetti da PDF.
* **Elimina riferimenti incrociati esterni**: Rimuove i collegamenti ad altri documenti. I collegamenti che si spostano in altre posizioni all’interno di PDF non vengono rimossi.
* **Elimina Il Contenuto Del Livello Nascosto E I Livelli Visibili Flatten**: Diminuisce la dimensione del file. Il documento ottimizzato assomiglia al PDF originale ma non contiene informazioni sul livello.
* **Elimina Informazioni E Metadati Documento**: Rimuove le informazioni nel dizionario delle informazioni del documento e in tutti i flussi di metadati. (Utilizzare il comando Salva con nome per ripristinare i flussi di metadati in una copia di PDF.)
* **Elimina allegati file**: Rimuove tutti gli allegati di file, compresi gli allegati aggiunti al PDF come commenti. (PDF Optimizer non ottimizza i file allegati.)
* **Elimina Dati Privati Di Altre Applicazioni**: Elimina le informazioni da un documento di PDF che sono utili solo per l’applicazione che ha creato il documento. Questa impostazione non influisce sulla funzionalità di PDF, ma riduce la dimensione del file.

### Pulisci {#clean-up}

Seleziona **Pulisci** per rimuovere elementi non necessari dal documento.
Questi elementi includono elementi obsoleti o non necessari per l&#39;uso previsto del documento. La rimozione di alcuni elementi può influire gravemente sulla funzionalità di PDF. Per impostazione predefinita, vengono selezionati solo gli elementi che non influiscono sulla funzionalità. Se non sei sicuro delle implicazioni della rimozione di altre opzioni, utilizza le selezioni predefinite.

**Compressione**

Selezionare una delle seguenti opzioni di compressione Flate dal menu a discesa:

* Comprimi l&#39;intero file
* Comprimi la struttura del documento
* Rimuovi compressione
* Lascia la compressione intatta

**Utilizza Flate Per Codificare I Flussi Non Codificati**: Applica la compressione Flate a tutti i flussi che non sono codificati.

**Elimina segnalibri non validi**: Rimuove i segnalibri che puntano alle pagine del documento che vengono eliminate.

**Elimina destinazioni con nome senza riferimenti**: Rimuove dall’interno del documento PDF le destinazioni con nomi alle quali non viene fatto riferimento internamente. Questa opzione non verifica la presenza di collegamenti da altri file o siti web di PDF.

**Ottimizzare PDF Per La Visualizzazione Web Rapida**: Ristruttura un documento PDF per il download della pagina alla volta (byte-serving) dai server web.

**Nei Flussi Che Utilizzano La Codifica LZW, Utilizza Invece Flate**: Applica la compressione Flate a tutti i flussi di contenuto e alle immagini che utilizzano la codifica LZW.

**Elimina collegamenti non validi**: Rimuove i collegamenti che passano a destinazioni non valide.

**Ottimizzare il contenuto della pagina**: Converte tutti i caratteri di fine riga in caratteri di spazio, migliorando la compressione Flate.

## Impostazioni di Microsoft Excel (solo Windows) {#microsoft-excel-settings-windows-only}

Queste opzioni determinano il modo in cui i file di Microsoft Excel vengono convertiti. Per istruzioni su come accedere a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

**Prova OpenOffice come convertitore di fallback**: Quando questa opzione è selezionata e una conversione che utilizza Microsoft Excel non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, viene scritta un&#39;eccezione nel file di registro.

**Estensioni nome file**: Specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per questa applicazione. Il valore predefinito è `xls,xlsx`. Non includere un punto prima o uno spazio tra le estensioni.

**Creare un file conforme a PDF/A-1a**: Forza l’utilizzo dell’impostazione Adobe PDF di PDF/A-1b:2005 RGB.

**Aggiungere Segnalibri Ad Adobe PDF**: Converte i nomi dei fogli di lavoro di Excel in segnalibri. Per impostazione predefinita, questa opzione è selezionata.

**Adatta foglio di lavoro a una singola pagina**: Riduce le dimensioni del testo per adattarlo al foglio di lavoro su una singola pagina.

**Converti intera cartella di lavoro**: Converte tutti i fogli di lavoro nel file Excel. Se questa opzione non è selezionata, viene convertita solo la pagina corrente.

**Esegui macro automaticamente**: Esegue qualsiasi macro nel documento Excel, ad esempio una macro che inserisce l&#39;ora corrente, prima di convertire il documento.

**Converti informazioni documento**: Aggiunge proprietà del documento PDF in base alle informazioni del documento nel file di origine. Sono incluse informazioni quali titolo del documento, autore, oggetto e parole chiave.

**Aggiungere Collegamenti Ad Adobe PDF**: Converte i collegamenti ipertestuali nel file di origine in collegamenti ipertestuali nel documento di PDF.

**Allega File Di Origine Ad Adobe PDF**: Quando questa opzione è selezionata, il foglio di calcolo Excel originale viene inserito come allegato all’interno del documento PDF generato.

**Abilita Accessibilità E Reflow Con Adobe PDF Con Tag**: Incorpora i tag all’interno del documento PDF per abilitare l’accessibilità e il riflusso.

**Elenco Di Componenti Aggiuntivi Excel Da Caricare**: Per impostazione predefinita, per motivi di sicurezza, non vengono eseguiti componenti aggiuntivi di Excel quando un file Excel viene convertito in PDF. Per consentire l&#39;esecuzione di alcuni componenti aggiuntivi di Excel durante la conversione, fornisci un elenco separato da virgole dei nomi dei componenti aggiuntivi.

**Elenco Di Fogli Di Lavoro Da Convertire**: Quando questa casella è vuota, tutti i fogli di lavoro del foglio di calcolo Excel vengono inclusi nel PDF generato. Per convertire in modo selettivo un sottoinsieme dei fogli di lavoro, fornire un elenco separato da virgole dei nomi dei fogli di lavoro.

## Impostazioni di Microsoft PowerPoint (solo Windows) {#microsoft-powerpoint-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file Microsoft PowerPoint. Per istruzioni su come accedere a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Prova OpenOffice come convertitore di fallback]**: Quando questa opzione è selezionata e una conversione che utilizza Microsoft PowerPoint non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, viene scritta un&#39;eccezione nel file di registro.

**[!UICONTROL Estensioni nome file]**: Specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per questa applicazione. Il valore predefinito è ppt, pptx. Non includere un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni documento]**: Aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, tra cui titolo, oggetto, autore, parole chiave, manager, azienda, categoria e commenti. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Aggiungere Segnalibri Ad Adobe PDF]**: Converte i titoli di PowerPoint in segnalibri. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Allega File Di Origine Ad Adobe PDF]**: Aggiunge il file di origine al file PDF come allegato. Per impostazione predefinita questa opzione è deselezionata.

**[!UICONTROL Abilita Accessibilità E Reflow Con Adobe PDF Con Tag]**: Incorpora i tag nel file PDF. Per impostazione predefinita questa opzione è deselezionata.

**[!UICONTROL Convertire Multimedia In PDF Multimedia]**: Converte i file multimediali in file multimediali PDF, ove possibile. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Converti note speaker]**: Converte le note dei diffusori in PDF.

**[!UICONTROL Esegui macro automaticamente]**: Esegue qualsiasi macro nel documento di PowerPoint, ad esempio una macro che inserisce l&#39;ora corrente, prima di convertire il documento.

**[!UICONTROL Layout PDF basato sulle impostazioni della stampante PowerPoint]**: Utilizza le impostazioni della stampante PowerPoint per impostare il layout del documento PDF.

**[!UICONTROL Aggiungere Collegamenti Ad Adobe PDF]**: Mantiene i collegamenti esistenti quando il file viene convertito. L’aspetto dei collegamenti è generalmente invariato. I collegamenti possono essere creati solo se è selezionata anche l’opzione Abilita accessibilità . Per impostazione predefinita questa opzione è deselezionata.

**[!UICONTROL Salvare Le Transizioni Diapositive In Adobe PDF]**: Converte le transizioni delle diapositive. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Salvataggio Di Animazioni In Adobe PDF]**: Salva le animazioni convertite nel file PDF.

**[!UICONTROL Convertire Diapositive Nascoste In Pagine PDF]**: Converte le diapositive nascoste.

**[!UICONTROL Creare un file conforme a PDF/A-1a]**: Forza l’utilizzo dell’impostazione Adobe PDF di PDF/A-1b:2005 RGB. Alcune funzionalità di PowerPoint non vengono convertite quando si produce un file PDF. Se una transizione PowerPoint non ha una transizione equivalente in Acrobat, viene sostituita una transizione simile. Se più effetti di animazione si trovano nella stessa diapositiva, viene utilizzato un singolo effetto. Le transizioni di pagina e i plug-in vengono convertiti.

## Impostazioni progetto Microsoft (solo Windows) {#microsoft-project-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di progetto Microsoft. Per istruzioni su come accedere a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

1. **[!UICONTROL Estensioni nome file:]** Specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per questa applicazione. Il valore predefinito è `mpp`. Non includere un punto prima o uno spazio tra le estensioni.

1. **[!UICONTROL Converti informazioni documento]**: Aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, tra cui titolo, oggetto, autore, parole chiave, manager, azienda, categoria e commenti. Per impostazione predefinita, questa opzione è selezionata.
1. **[!UICONTROL Allega File Di Origine Ad Adobe PDF]**: Aggiunge il file di origine al file PDF come allegato.
1. **[!UICONTROL Creare un file conforme a PDF/A-1a]**: Forza l’utilizzo dell’impostazione Adobe PDF di PDF/A-1b:2005 RGB.
1. **[!UICONTROL Esegui macro automaticamente]**: Esegue qualsiasi macro nel documento Progetto Microsoft (ad esempio una macro che inserisce l&#39;ora corrente) prima di convertire il documento.

## Impostazioni di Microsoft Word (solo Windows) {#microsoft-word-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft Word. Per istruzioni su come accedere a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

**[!UICONTROL Prova OpenOffice come convertitore di fallback]**: Quando questa opzione è selezionata e una conversione che utilizza Microsoft Word non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, viene scritta un&#39;eccezione nel file di registro.

**[!UICONTROL Estensioni nome file]**: Specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per questa applicazione. Il valore predefinito è `doc,docx,rtf,txt`. Non includere un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni documento]**: Aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, tra cui titolo, oggetto, autore, parole chiave, manager, azienda, categoria e commenti. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Aggiungere Segnalibri Ad Adobe PDF]**: Converte i titoli in segnalibri. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Allega File Di Origine Ad Adobe PDF]**: Aggiunge il file di origine al file PDF come allegato.

**[!UICONTROL Convertire Riferimenti E Sommario In Collegamenti]**: Converte tutti i riferimenti incrociati e le voci del sommario in collegamenti. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Abilita Accessibilità E Reflow Con Adobe PDF Con Tag]**: Incorpora i tag nel file PDF. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Creare un file conforme a PDF/A-1a]**: Se selezionata, forza l’utilizzo dell’impostazione Adobe PDF di PDF/A-1b:2005 RGB.

**[!UICONTROL Esegui macro automaticamente]**: Esegue qualsiasi macro nel documento di Word, ad esempio una macro che inserisce l&#39;ora corrente, prima di convertire il documento.

**[!UICONTROL Mantieni Marcatura Documento In Adobe PDF]**: Converte il markup nel documento Word in annotazioni nel file PDF.

**[!UICONTROL Aggiungere Collegamenti Ad Adobe PDF]**: Converte i collegamenti ipertestuali nel file di origine in collegamenti ipertestuali nel documento di PDF.

**[!UICONTROL Conversione Di Collegamenti A Note A Piè Di Pagina E A Note Di Chiusura]**: Crea collegamenti dalle note a piè di pagina e di chiusura alle note nel documento di PDF.

**[!UICONTROL Conversione di commenti visualizzati in note in Adobe PDF]**: Converte i commenti nel documento Word in note di testo nel documento PDF.

**[!UICONTROL Abilita assegnazione tag avanzati]**: Aggiunge tag avanzati per una migliore accessibilità.

**[!UICONTROL Convertire Tutti Gli Stili In Segnalibri]**: Converte tutti gli stili nel documento Word in segnalibri nel documento PDF.

**[!UICONTROL Converti stili specificati in segnalibri]**: Converte gli stili definiti nel **[!UICONTROL Stili con livelli]** ai segnalibri nel documento PDF.

**[!UICONTROL Stili Con Livelli]**: Specifica gli stili del documento Word convertiti in segnalibri nel documento PDF. Specifica anche il livello dei segnalibri. Per utilizzare questa funzione, deseleziona la **[!UICONTROL Convertire Tutti Gli Stili In Segnalibri]** e specificare i nomi degli stili nel formato seguente:

**styleName1=level1[,styleName2=level2...]**

Se un nome di stile di Microsoft Word include una virgola (,) o un segno di uguale (=), anteporre i caratteri speciali al carattere di escape (&quot;\_). Ad esempio, specificare uno stile denominato &quot;Titolo, 1&quot; come Intestazione\, 1.

**Codifica Acrobat PDFMaker:** Specifica il tipo di codifica dei file di testo normale di input in Acrobat PDFMaker. Ad esempio, se utilizzi un file con codifica UTF-8, seleziona UTF-8 per ottenere risultati migliori.

## Impostazioni di Microsoft Visio (solo Windows) {#visio}

**Converti informazioni documento**: Aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, tra cui titolo, oggetto, autore, parole chiave, manager, azienda, categoria e commenti. Per impostazione predefinita, questa opzione è selezionata. Questa opzione è attivata per impostazione predefinita.

**Aggiungere Collegamenti Ad Adobe PDF**: Mantiene tutti i collegamenti. Per impostazione predefinita, questa opzione è selezionata.

**Aggiungere Segnalibri Ad Adobe PDF**: Converte i titoli in segnalibri. Per impostazione predefinita, questa opzione è selezionata.

**Allega File Di Origine Ad Adobe PDF**: Aggiunge il file di origine al file PDF come allegato.

**Flatten Always Layers In Adobe PDF**: Flattisce tutti i livelli di Visio.

**Converti tutte le pagine**: Converte tutte le pagine del file Visio.

**Apri Il Pannello Livelli Quando Visualizzato In Adobe Acrobat**: Se i livelli di Visio non sono appiattiti, apre una finestra in cui è possibile specificare i livelli che vengono mantenuti nel file PDF quando vengono aperti con Acrobat. Per impostazione predefinita, questa opzione è selezionata.

**Creare file conformi a PDF/A-1b**: Impone l’utilizzo di Adobe PDF Setting PDF/A-1b:2005 (RGB).

**Convertire Commenti In Commenti Adobe PDF**: Converte le note di Visio in commenti di PDF.

## Impostazioni di Microsoft Publisher (solo Windows) {#microsoft-publisher-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft Publisher. Per istruzioni su come accedere a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

**[!UICONTROL Estensioni nome file]**: Specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per questa applicazione. Il valore predefinito è `pub`. Non includere un punto prima o uno spazio tra le estensioni.

## Impostazioni AutoCAD (solo Windows) {#autocad-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file AutoCAD. Per istruzioni su come accedere a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Estensioni nome file]**: Specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per questa applicazione. Il valore predefinito è `dwg`. Non includere un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni documento]**: Aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, tra cui titolo, oggetto, autore, parole chiave, manager, azienda, categoria e commenti. Per impostazione predefinita, questa opzione è selezionata.

**[!UICONTROL Aggiungere Segnalibri Ad Adobe PDF]**: Converte i titoli in segnalibri.

**[!UICONTROL Flatten Always Layers In Adobe PDF]**: Riflette tutti i livelli AutoCAD.

**[!UICONTROL Apre Il Riquadro Livelli Visualizzato In Adobe Acrobat]**: Mostra la struttura dei livelli quando PDF viene aperto in Acrobat.

**[!UICONTROL Converti tutti i layout]**: Include tutti i layout in PDF.

**[!UICONTROL Converti spazio modello in 3D]**: Se selezionata, il layout dello spazio del modello viene convertito in un&#39;annotazione 3D in PDF.

**[!UICONTROL Aggiungere Collegamenti Ad Adobe PDF]**: Se selezionato, conserva tutti i collegamenti.

**[!UICONTROL Allega File Di Origine Ad Adobe PDF]**: Aggiunge il file di origine al file PDF come allegato.

**[!UICONTROL Creare file conformi a PDF/A-1b]**: Forza l’utilizzo dell’impostazione Adobe PDF PDF/A-1b.

**[!UICONTROL Converti tutti i livelli]**: Per impostazione predefinita, PDF Generator converte in PDF solo il livello predefinito dei file AutoCAD anziché tutti i livelli presenti nel file. Selezionare questa opzione per convertire tutti i livelli del file.

**[!UICONTROL Informazioni sulla scala di incorporamento]**: Mantiene le informazioni sulla scala del disegno.

**[!UICONTROL Converti layout corrente]**: Include solo il layout corrente in PDF.

**[!UICONTROL Elenco dei layout AutoCAD da convertire]**: Un disegno AutoCAD può avere più layout. Quando questa casella è vuota, tutti i layout del disegno AutoCAD vengono inclusi nel documento PDF generato. Per convertire in modo selettivo un sottoinsieme dei layout, fornisci un elenco di nomi di layout separati da virgola.

## Impostazioni di OpenOffice {#openoffice-settings}

Queste opzioni determinano la modalità di conversione dei file OpenOffice. Per istruzioni su come accedere a queste opzioni, consulta [Creare o modificare le impostazioni del tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Prova PDFMaker come convertitore di fallback**: Quando questa opzione è selezionata e una conversione che utilizza OpenOffice non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando PDFMaker. Se la conversione con PDFMaker non riesce o raggiunge il limite di timeout specificato, viene scritta un&#39;eccezione nel file di registro.

**Estensioni nome file**: Specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per questa applicazione. Il valore predefinito è `odt,odp,ods,odg,odf,sxw,sxi,sxd`. Non includere un punto prima o uno spazio tra le estensioni.

**Intervallo**: Converti tutte le pagine o specifica pagine particolari o un intervallo di pagine. Se un intervallo di pagine non è definito, tutte le pagine vengono convertite. Per esportare un intervallo di pagine, utilizza il formato 3-6. Per esportare pagine singole, utilizza il formato 7;9;11. È possibile esportare una combinazione di intervalli di pagine e pagine singole utilizzando un formato come 3-6;8;10;12.

**Orientamento pagina**: Solo per i file di testo normale, selezionare verticale o orizzontale per il documento PDF convertito.

**Immagini**: Configura la modalità di conversione delle immagini. Le immagini EPS con anteprime incorporate vengono esportate solo come anteprime. Le immagini EPS senza anteprime incorporate vengono esportate come segnaposto vuoti. Con una compressione senza perdita di immagini, tutti i pixel vengono conservati. Con la compressione JPEG delle immagini e un livello di alta qualità, quasi tutti i pixel vengono conservati. Con un livello di bassa qualità, alcuni pixel vengono persi e gli artefatti vengono introdotti, ma le dimensioni dei file sono ridotte.

**Generale**: Abilitare le opzioni per convertire un PDF con tag o per esportare le note dei documenti Writer e FormCalc, Imprimere gli effetti di transizione delle diapositive o le pagine vuote in PDF. Quando i tag vengono esportati, la dimensione del file può aumentare di grandi dimensioni. Alcuni tag esportati sono sommario, collegamenti ipertestuali e controlli.

È inoltre possibile specificare la modalità di invio dei moduli. Le opzioni sono XML, FDF, PDF o HTML. Questa impostazione sostituisce la proprietà URL del controllo impostata nel documento. Per il documento PDF è possibile selezionare una sola impostazione comune:

* PDF (invia l&#39;intero documento)
* FDF (invia il contenuto del controllo)
* HTML
* XML

**PDF con tag**: Abilita la creazione di PDF con tag dai documenti OpenOffice. PDF con tag contiene informazioni sulla struttura del contenuto del documento. Questo può essere utile quando il documento viene visualizzato su dispositivi con schermate diverse e quando si utilizza un software per l’utilità di lettura dello schermo. Consente inoltre al software di accesso facilitato di eseguire varie operazioni utili con il documento di PDF, ad esempio la lettura ad alta voce dei contenuti del documento di PDF.

**Note sull’esportazione**: Converte le note nei documenti OpenOffice in note nel documento PDF generato.

**Usa effetti di transizione**: Converte gli effetti di transizione della diapositiva nelle presentazioni OpenOffice agli effetti di transizione di PDF corrispondenti.

**Invia Forms in formato**: Crea un modulo PDF che può essere compilato e stampato dall’utente del documento PDF.

**Esporta automaticamente le pagine vuote inserite**: Quando questa opzione è selezionata, le pagine vuote inserite automaticamente vengono incluse nel documento PDF generato. Questa opzione è utile se si stampa un documento PDF fronte/retro. Ad esempio, è possibile configurare un libro in modo che la prima pagina del capitolo inizi sempre su una pagina dispari. Se il capitolo precedente termina su una pagina dispari, OpenOffice imposta una pagina pari vuota. Questa opzione controlla se includere la pagina pari nel PDF generato.

## Altre impostazioni dell&#39;applicazione (solo Windows) {#other-applications-settings-windows-only}

Non è possibile modificare le impostazioni per altre applicazioni tramite la console di amministrazione; visualizzano le estensioni del nome file per i tipi di file supportati. Per istruzioni su come accedere a queste impostazioni, consulta [Creare o modificare le impostazioni del tipo di file](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* Adobe PageMaker: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Potrebbe essere necessario personalizzare il supporto per questi tipi di file. Per ulteriori informazioni, consulta &quot;Aggiunta di supporto per formati di file nativi aggiuntivi&quot; in [Programmazione con moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_62).

Per informazioni sulla configurazione di una stampante di rete PDFG, vedere [Configurazione di una stampante di rete PDFG (solo Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
