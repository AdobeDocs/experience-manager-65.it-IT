---
title: Configurazione delle impostazioni del tipo di file
description: Scopri come configurare le impostazioni del tipo di file. In PDF Generator è possibile impostare le impostazioni dell'applicazione per i tipi di file supportati per configurare le impostazioni dei tipi di file.
uuid: ab037659-c6ff-4de9-9417-f5a6fc8122cb
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ab19b248-8931-4cf6-b6a5-fb7b067c4a49
feature: PDF Generator
exl-id: 1a6640cc-22ef-41d5-a0c6-7a2c2dabcef1
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '6176'
ht-degree: 0%

---

# Configurazione delle impostazioni del tipo di file {#configuring-file-type-settings}

In PDF Generator è possibile impostare le impostazioni dell&#39;applicazione per i tipi di file supportati. In Windows è possibile impostare le impostazioni dell&#39;applicazione per ogni tipo di file supportato. In UNIX e Linux è possibile impostare le impostazioni dell&#39;applicazione per HTML-to-PDF e OpenOffice.

Nella pagina Impostazioni tipo di file è possibile eseguire le operazioni riportate di seguito.

* [Creare o modificare un&#39;impostazione di Tipo file](#create-or-edit-file-type-settings)
* Specificare le impostazioni del tipo di file da utilizzare per impostazione predefinita (vedere [Importazione ed esportazione dei file di configurazione di PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md))
* [Modificare le impostazioni predefinite](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)
* [Abilita supporto PDF/A](/help/forms/using/admin-help/enable-pdf-a-support.md)
* [Eliminare un&#39;impostazione di tipo file](/help/forms/using/admin-help/enable-pdf-a-support.md)

>[!NOTE]
>
>Le impostazioni del tipo di file non sono disponibili per i convertitori di fallback come Acrobat per la conversione da HTML a PDF, Microsoft PowerPoint, Microsoft Word e Microsoft Excel.

## Creare o modificare le impostazioni del tipo di file {#create-or-edit-file-type-settings}

Creare o modificare un&#39;impostazione del tipo di file per specificare il modo in cui l&#39;applicazione gestisce la conversione dei tipi di file supportati. In Windows è possibile impostare le impostazioni dell&#39;applicazione per ogni tipo di file supportato. In UNIX e Linux è possibile impostare le impostazioni dell&#39;applicazione per HTML-to-PDF e OpenOffice.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Servizi]** > **[!UICONTROL PDF Generator]** > **[!UICONTROL Impostazioni tipo di file]**.
1. Fai clic su Nuovo o sul nome di un’impostazione.
1. Nella casella Estensioni nome file digitare le estensioni del nome file, separate da virgole, per i tipi di file accettati per l&#39;applicazione. Non includere il periodo prima o uno spazio tra le estensioni. Il valore predefinito è `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Facoltativo) Per utilizzare il riconoscimento del codice ottico (OCR) del testo in immagini o immagini, selezionate Usa OCR (Use OCR) e impostate le seguenti opzioni:

**Lingua OCR primaria:** Lingua utilizzata dal motore OCR per identificare i caratteri. Il valore predefinito è Inglese (Stati Uniti).

**Stile di output PDF:** Selezionare Immagine ricercabile per avere un&#39;immagine bitmap delle pagine in primo piano e il testo digitalizzato su un livello invisibile sottostante. L’aspetto della pagina non cambia, ma il testo diventa selezionabile e leggibile. Selezionare Testo e grafica formattati per ricostruire la pagina originale utilizzando testo, caratteri, immagini e altri elementi grafici riconosciuti. L&#39;impostazione predefinita è Immagine ricercabile (esatta).

**Downsampling immagini:** Diminuisce il numero di pixel nelle immagini a colori, in scala di grigi e monocromatiche. Il downsampling delle immagini digitalizzate viene eseguito dopo il completamento dell&#39;OCR. Il valore predefinito è Minore (600 dpi). Questa opzione non è disponibile se lo stile di output PDF è impostato su Immagine ricercabile (esatta).

1. Compila le informazioni richieste nelle sezioni seguenti:

[Importazione ed esportazione dei file di configurazione di PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)

[Impostazioni di esportazione Adobe PDF (solo Windows)](#adobe-pdf-export-settings-windows-only)

[Impostazioni HTML-PDF](#html-to-pdf-settings)

[Flash video in impostazioni PDF](#flash-videos-to-pdf-settings)

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

   Per passare a un’altra sezione, fai clic sul relativo collegamento nella pagina web o utilizza **[!UICONTROL Successivo]** o **[!UICONTROL Precedente]** pulsanti.

1. Dopo aver completato tutte le sezioni, fai clic su **[!UICONTROL Salva]** o **[!UICONTROL Salva con nome]** e fornisci un nome per l’impostazione.

È possibile personalizzare il supporto per vari tipi di file. (Vedere &quot; [Aggiunta del supporto per formati di file nativi aggiuntivi](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot; in [Programmazione con i moduli AEM](https://www.adobe.com/go/learn_lc_programming_11).)

## Modificare le impostazioni predefinite {#change-the-default-settings}

È possibile modificare il valore predefinito per le impostazioni di Adobe PDF, le impostazioni di protezione e le impostazioni del tipo di file applicabili alle nuove origini create. La modifica dei valori predefiniti non influisce sulle impostazioni delle origini esistenti.

1. In Administration Console, fai clic su **[!UICONTROL Servizi > PDF Generator]**.
1. Il giorno **[!UICONTROL Impostazioni Adobe PDF]**, **[!UICONTROL Impostazioni tipo di file]**, o **[!UICONTROL Impostazioni di protezione]** pagina, fai clic su **[!UICONTROL Imposta impostazioni predefinite]**.
1. Seleziona le impostazioni predefinite preferite. Nella pagina Imposta impostazioni predefinite sono disponibili una o più delle seguenti impostazioni:

   **[!UICONTROL Impostazione Adobe PDF]**: l’impostazione predefinita originale è Standard (Acrobat 6).

   **[!UICONTROL Impostazioni di protezione]**: il valore predefinito originale è No Security (Acrobat 5).

   **[!UICONTROL Impostazioni tipo di file]**: il valore predefinito originale è Standard.

1. Fai clic su **[!UICONTROL Salva]**.

## Eliminare un&#39;impostazione di tipo file {#delete-a-file-type-setting}

È possibile eliminare un&#39;impostazione del tipo di file non più utilizzata.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Servizi > PDF Generator > Impostazioni tipo di file]**.
1. Selezionare la casella di controllo accanto all&#39;impostazione da eliminare. È possibile selezionare più origini. Le impostazioni prive di una casella di controllo accanto a esse sono sempre incluse in PDF Generator e non possono essere eliminate.
1. Clic **[!UICONTROL Elimina]** e nella pagina Conferma eliminazione fai clic su **[!UICONTROL Elimina]**.

## Impostazioni immagine per PDF {#image-to-pdf-settings}

Le seguenti opzioni determinano la modalità di conversione dei file di immagine in PDF. Per istruzioni sull&#39;accesso a queste impostazioni, vedere [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Estensioni nome file:** Elenco separato da virgole delle estensioni dei nomi di file che possono essere convertite.

**Prova Fallback Converter:** PDF Generator può utilizzare Java™ o Acrobat per convertire i file immagine in PDF. Quando questa opzione è selezionata e una conversione non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando il metodo alternativo. Se il metodo alternativo non riesce o raggiunge il limite di timeout specificato, nel file di log viene scritta un&#39;eccezione.

>[!NOTE]
>
>I file JPEG 2000 possono essere convertiti solo con Acrobat.

**Usa OCR:** Specifica se applicare OCR (riconoscimento ottico dei caratteri) al PDF. Il software OCR consente di cercare, correggere e copiare il testo nel PDF.

***nota **: la funzionalità PDF OCR (PDF ricercabile) è supportata solo in Microsoft Windows.*

**Lingua OCR primaria:** Specifica la lingua utilizzata dal motore OCR per identificare i caratteri.

**Stile di output PDF:** Determina il tipo di PDF da produrre. Tutti i formati consentono di applicare il riconoscimento OCR e font e pagina alle immagini di testo e di convertirle in testo normale.

**Immagine ricercabile:** Garantisce che il testo possa essere cercato e selezionato. Questa opzione mantiene l&#39;immagine originale, la disegna in base alle esigenze e posiziona sopra di essa un livello di testo invisibile. L’opzione Downsampling immagini determina se l’immagine viene ricampionata verso il basso e in quale misura.

**Immagine ricercabile (esatta):** Garantisce che il testo possa essere cercato e selezionato. Questa opzione mantiene l&#39;immagine originale e posiziona sopra di essa un livello di testo invisibile. Consigliato per i casi che richiedono la massima fedeltà all’immagine originale.

**ClearScan:** Sintetizza un nuovo font Type 3 che si avvicina molto all&#39;originale e mantiene lo sfondo della pagina utilizzando una copia a bassa risoluzione.

**Downsampling immagini:** Diminuisce il numero di pixel nelle immagini a colori, in scala di grigi e monocromatiche dopo il completamento dell&#39;OCR. Scegliere il livello di downsampling da applicare. Le opzioni con numero più alto riducono il downsampling, generando PDF con risoluzione più elevata.

## Impostazioni di esportazione Adobe PDF (solo Windows) {#adobe-pdf-export-settings-windows-only}

L’impostazione Esporta tipo di file nella sezione Impostazioni di esportazione di Adobe PDF viene utilizzata per convertire un file PDF in un altro formato. Il valore predefinito è HTML 4.01 con fogli di stile CSS 1.0 (*.htm, *.html).

Per istruzioni sull&#39;accesso a questa impostazione, vedere [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Impostazioni HTML-PDF {#html-to-pdf-settings}

Le opzioni seguenti determinano la modalità di conversione dei file HTML in PDF. Per istruzioni sull&#39;accesso a queste opzioni, vedere [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Prova Fallback Converter:** PDF Generator può utilizzare Java™ o Acrobat per convertire i file HTML in PDF. Quando questa opzione è selezionata e una conversione non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando il metodo alternativo. Se il metodo alternativo non riesce o raggiunge il limite di timeout specificato, nel file di log viene scritta un&#39;eccezione.

**Codifica predefinita:** Imposta la codifica di input del testo del file da un menu di sistemi operativi e alfabeti. Utilizza la selezione mostrata nell&#39;opzione Codifica predefinita solo se il file di origine di HTML non specifica un tipo di codifica.

**Forza codifica selezionata:** Ignora qualsiasi codifica specificata nel file di origine di HTML e utilizza la selezione mostrata nell&#39;opzione Codifica predefinita.

### Impostazioni di spider {#spidering-settings}

*Spider* analizza le pagine web alla ricerca di collegamenti ad altre pagine web. Quando viene rilevato un collegamento a un’altra pagina web, la pagina di destinazione viene recuperata e inclusa nel documento PDF generato. Abilita queste opzioni per impostare il numero di livelli da recuperare e convertire in PDF:

**Ottieni Solo Livelli X:** Spider e converte le pagine fino a una profondità del livello specificato dall&#39;URL della pagina base. Un valore pari a 1 converte solo l’URL specificato.

**Ottieni intero sito:** Converte l’intero sito, a partire dall’URL fornito.

**Rimani Sullo Stesso Percorso:** Eventuali collegamenti che puntano a pagine che non si trovano nello stesso percorso relativo dell’URL di base non vengono convertiti durante il spider.

**Rimani sullo stesso server:** Eventuali collegamenti che puntano a pagine su server diversi non vengono convertiti durante il spider. Vengono convertiti solo i collegamenti che puntano allo stesso server dell’URL specificato.

### Impostazioni di conversione pagina {#page-conversion-settings}

Abilita queste opzioni per specificare la modalità di conversione delle pagine HTML. In base alle dimensioni della pagina, i valori di larghezza, altezza e margine vengono modificati di conseguenza.

**Dimensioni pagina:** Scegliete custom e specificate la larghezza e l&#39;altezza, oppure selezionate le quote predefinite.

**Orientamento:** Selezionare Verticale o Orizzontale per il documento PDF convertito.

**Margini:** Specifica i margini (Superiore, Inferiore, Sinistro e Destro) nel documento PDF generato.

**Aggiungi Segnalibri A PDF:** Aggiunge segnalibri al documento PDF.

**Abilita PDF con tag:** Incorpora i tag nel documento PDF.

**Imposta impostazioni visualizzazione iniziale:** Consente di configurare le opzioni documento, finestra e interfaccia utente. Queste impostazioni determinano la modalità di visualizzazione iniziale del contenuto.

### Opzioni documento {#document-options}

Abilitare queste opzioni per specificare come visualizzare il contenuto, come visualizzare le pagine nel documento PDF e come specificare il livello di ingrandimento:

**Mostra:** Seleziona i riquadri da aprire in Acrobat quando viene aperto il documento PDF.

**Layout pagina:** Selezionare il tipo di layout di pagina per il documento PDF.

**Ingrandimento:** Scegliere l&#39;ingrandimento predefinito per la visualizzazione iniziale del documento PDF oppure selezionare un valore personalizzato. La scelta di un&#39;impostazione predefinita indica che viene utilizzato l&#39;ingrandimento predefinito di Acrobat.

**Apri a numero pagina:** Specifica il numero di pagina a cui il PDF si apre.

### Opzioni finestra {#window-options}

Abilitare queste opzioni per specificare le dimensioni e la visualizzazione della finestra.

**Ridimensiona finestra alla pagina iniziale:** Ridimensiona la finestra di Acrobat alle dimensioni della pagina iniziale.

**Centro finestra su schermo:** Apre la finestra al centro dello schermo.

**Apri In Modalità A Schermo Intero:** Apre la finestra in modalità a schermo intero.

**Mostra:** Visualizza il titolo o il nome del documento nella finestra.

### Opzioni interfaccia utente {#user-interface-options}

Abilitare queste opzioni per specificare l&#39;aspetto della finestra:

**Nascondi barra dei menu:** Nasconde la barra dei menu nel documento di PDF.

**Nascondi barre degli strumenti:** Nasconde le barre degli strumenti nel documento PDF.

**Nascondi controlli finestra:** Nasconde i controlli della finestra nel documento PDF.

## Flash video in impostazioni PDF {#flash-videos-to-pdf-settings}

PDF Generator supporta la possibilità di inviare un video, ad Adobe un Flash (file SWF o FLV) e di creare un file PDF con un video, ad Adobe un Flash incorporato. Questa conversione non richiede l&#39;installazione del Flash Player Adobe nel server Forms. Per istruzioni sull’accesso a questa opzione, consulta [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Estensioni nome file:** Elenco separato da virgole delle estensioni dei nomi di file che possono essere convertite.

## Impostazioni da XPS a PDF {#xps-to-pdf-settings}

XPS (XML Paper Specification) viene utilizzato in un computer di stampa Windows. Questo è un formato Microsoft e può essere creato da qualsiasi applicazione di Microsoft Office. I moduli AEM consentono di convertire i file XPS PDF.

**Estensioni nome file:** Un elenco separato da virgole di tutte le estensioni del nome file XPS che possono essere convertite. Attualmente esiste un formato: .xps.

## Impostazioni di PDF Optimizer {#pdf-optimizer-settings}

PDF Generator supporta la possibilità di ridurre le dimensioni dei file PDF. L&#39;utilizzo di tutte queste impostazioni o solo di alcune dipende dal modo in cui si intende utilizzare i file e dalle proprietà essenziali di un file. Nella maggior parte dei casi, le impostazioni predefinite sono appropriate per la massima efficienza: consente di risparmiare spazio rimuovendo i font incorporati, comprimendo le immagini e rimuovendo gli elementi dai file che non sono più necessari.

>[!NOTE]
>
>L&#39;ottimizzazione di un documento con firma digitale rimuove e invalida le firme digitali.

Per istruzioni sull&#39;accesso a questa impostazione, vedere [Creare o modificare le impostazioni del tipo di file](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Versione di Target PDF:** Specifica la versione di Acrobat con cui il PDF è compatibile.

### Font {#fonts}

1. Seleziona **Font.**
1. Selezionare una delle opzioni seguenti:

   **Annulla l&#39;incorporamento di tutti i font:** Annulla l&#39;incorporamento di tutti i font incorporati.

   **Non annullare l&#39;incorporamento di alcun tipo di carattere:** Non annulla l&#39;incorporamento di font.

   **Annulla l&#39;incorporamento di alcuni tipi di carattere:** Annulla l&#39;incorporamento solo dei caratteri specificati. Per specificare i tipi di carattere che si desidera annullare l&#39;incorporamento, effettuare le operazioni riportate di seguito.

   * Se necessario, selezionare una directory dei font diversa dalla **Origine font** menu a discesa. Questo menu a discesa elenca le directory dei font specificate in **Home > Impostazioni > Sistema core > Configurazioni core**.
   * Selezionare uno o più tipi di carattere dal **Caratteri disponibili** e fai clic su **Aggiungi**. Questi font vengono aggiunti al **Caratteri da annullare l&#39;incorporamento** elenco.
   * Se si desidera annullare l&#39;incorporamento di alcuni tipi di carattere che non esistono nel server Forms, immettere i nomi di tali tipi di carattere nel **Aggiungi font per annullare l&#39;incorporamento** casella. Clic **Aggiungi**.

   >[!NOTE]
   >
   >*Se si desidera annullare l&#39;incorporamento di alcuni tipi di carattere i cui sottoinsiemi sono incorporati nel documento, anteporre al nome del tipo di carattere il segno +. Ad esempio, &quot;+Helvetica&quot;.*

1. Se desiderate incorporare solo i sottoinsiemi in uso dei font incorporati, selezionate **Sottoimposta tutti i font incorporati**.

   >[!NOTE]
   >
   >*Se utilizzi questa opzione in combinazione con **Annulla l&#39;incorporamento di alcuni tipi di carattere**, font in **Aggiungi font per annullare l&#39;incorporamento**L&#39;elenco è ancora completamente deincorporato.*

   >[!NOTE]
   >
   >*La creazione di sottoinsiemi di tipi di carattere è la tecnica di incorporamento di una sola porzione di un tipo di carattere. Un sottoinsieme di caratteri contiene solo i caratteri utilizzati nel documento.*

### Trasparenza {#transparency}

Se il documento PDF include un disegno che contiene trasparenza, è possibile utilizzare le impostazioni di PDF Optimizer per appiattire la trasparenza e ridurre le dimensioni del file.

>[!NOTE]
>
>Se Acrobat 4.0 e versioni successive sono selezionate come versione di Target PDF, tutti gli oggetti trasparenti vengono appiattiti. Per altre versioni di Target PDF, la trasparenza è supportata e puoi configurare le impostazioni di trasparenza.

Seleziona **Trasparenza** per configurare le impostazioni di trasparenza durante l&#39;ottimizzazione dei documenti PDF.

**Livello di trasparenza** Specifica la quantità di informazioni vettoriali da mantenere. Le impostazioni più alte mantengono più oggetti vettoriali, mentre le impostazioni più basse rasterizzano più oggetti vettoriali; le impostazioni intermedie mantengono aree semplici in forma vettoriale e rasterizzano quelli complessi. Selezionate l&#39;impostazione più bassa per rasterizzare tutti i disegni.

>[!NOTE]
>
>La quantità di rasterizzazione che si verifica dipende dalla complessità della pagina e dai tipi di oggetti sovrapposti.

**Testo e Line Art** Risoluzione con cui vengono rasterizzati tutti gli oggetti, incluse le immagini, il disegno vettoriale, il testo e le sfumature. I valori supportati sono da 1 pixel per pollice (ppi) a 9600 ppi.

>[!NOTE]
>
>La risoluzione Line Art e Text deve essere in genere impostata su 600-1200 ppi per fornire una rasterizzazione di alta qualità, in particolare su un tipo serif o di piccole dimensioni.

**Sfumatura e maglie** Risoluzione alla quale vengono rasterizzati il gradiente e le maglie. I valori supportati sono da 1 ppi a 1200 ppi.

>[!NOTE]
>
>La risoluzione di sfumatura e trama deve essere generalmente impostata su 150-300 ppi perché la qualità delle sfumature, delle ombre di rilascio e delle piume non migliora con risoluzioni più elevate, ma il tempo di stampa e le dimensioni del file aumentano.

**Converti tutto il testo in contorni** Converte tutti gli oggetti di tipo (tipo di punto, tipo di area e tipo di percorso) in contorni e elimina tutte le informazioni sul glifo di tipo nelle pagine contenenti trasparenza. Questa opzione garantisce che la larghezza del testo rimanga coerente durante la conversione. L&#39;attivazione di questa opzione provocherà un leggero spessore dei caratteri di piccole dimensioni se visualizzati in Acrobat o stampati su stampanti desktop a bassa risoluzione. Non influisce sulla qualità del tipo stampato su stampanti o fotounità ad alta risoluzione.

**Converti tutti i tratti in contorni** Converte tutti i tratti in semplici tracciati riempiti nelle pagine contenenti trasparenza. Questa opzione garantisce che la larghezza dei tratti rimanga costante durante l&#39;appiattimento. L&#39;attivazione di questa opzione determina un leggero spessore dei tratti sottili e può compromettere le prestazioni di appiattimento.

**Aree complesse del clip** Assicura che i limiti tra il disegno vettoriale e il disegno rasterizzato siano compresi lungo i percorsi degli oggetti. Questa opzione riduce gli artefatti di unione risultanti quando fanno parte di un registro

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Alcuni driver di stampa elaborano la grafica raster e la grafica vettoriale in modo diverso, talvolta con conseguente unione dei colori. È possibile ridurre al minimo i problemi di unione disattivando alcune impostazioni di gestione del colore specifiche per i driver di stampa. Le impostazioni variano a seconda della stampante; per ulteriori informazioni, consultare la documentazione fornita con la stampante.

Mantieni sovrastampa: fonde il colore della grafica trasparente con il colore di sfondo per creare un effetto di sovrastampa.

Nella tabella seguente sono illustrati i tipi di stampanti più comuni e la loro risoluzione misurata in dpi, la loro posizione predefinita dello schermo misurata in linee per pollice (lpi) e una risoluzione di ricampionamento per le immagini misurate in pixel per pollice (ppi). Se ad esempio si stampa su una stampante laser a 600 dpi, immettere 170 per la risoluzione con cui ricampionare le immagini.

**Immagini** Selezionate Immagini per specificare le opzioni di compressione e ricampionamento per le immagini a colori, in scala di grigi e monocromatiche. È possibile sperimentare queste opzioni per trovare un giusto equilibrio tra le dimensioni del file e la qualità dell&#39;immagine.L&#39;impostazione della risoluzione per le immagini a colori e in scala di grigio deve essere da 1,5 a 2 volte la risoluzione dello schermo a linee in corrispondenza della quale verrà stampato il file. La risoluzione per le immagini monocromatiche deve essere la stessa del dispositivo di output, ma è bene tenere presente che il salvataggio di un&#39;immagine monocromatica a una risoluzione superiore a 1500 dpi aumenta le dimensioni del file senza migliorare in modo significativo la qualità dell&#39;immagine. Le immagini che verranno ingrandite, ad esempio le mappe, potrebbero richiedere risoluzioni più elevate.

>[!NOTE]
>
>Il ricampionamento delle immagini monocromatiche può produrre risultati di visualizzazione imprevisti, ad esempio la mancata visualizzazione delle immagini. In questo caso, disattivare il ricampionamento e convertire nuovamente il file. Questo problema si verifica con maggiore probabilità con il sottocampionamento e con minore probabilità con il sottocampionamento bicubico.

<table>
 <tbody>
  <tr>
   <th><p><strong>Risoluzione della stampante</strong></p> </th>
   <th><p><strong>Schermata di riga predefinita</strong></p> </th>
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
* **Ignora Tutte Le Azioni Di Invio, Importazione E Reimpostazione Dei Moduli**: disabilita tutte le azioni relative all&#39;invio o all&#39;importazione dei dati del modulo e reimposta i campi del modulo. Questa opzione mantiene gli oggetti modulo a cui sono collegate le azioni.
* **Elimina tutte le azioni JavaScript**: rimuove dal PDF tutte le azioni che utilizzano JavaScript.
* **Ignora miniature pagina incorporate**: rimuove le miniature di pagina incorporate. Questa opzione è utile per i documenti di grandi dimensioni, che possono richiedere molto tempo per disegnare le miniature di pagina dopo aver fatto clic sul pulsante Pagine.
* **Converti linee smussate in curve**: riduce il numero di punti di controllo utilizzati per creare curve nei disegni CAD, riducendo le dimensioni dei file PDF e velocizzando il rendering sullo schermo.
* **Elimina impostazioni di stampa incorporate**: rimuove dal documento le impostazioni di stampa incorporate, ad esempio il ridimensionamento della pagina e la modalità fronte retro.
* **Elimina segnalibri**: rimuove tutti i segnalibri dal documento.
* **Appiattisci campi modulo**: rende inutilizzabili i campi modulo senza modificarne l’aspetto. I dati del modulo vengono uniti alla pagina per diventare contenuto della pagina.
* **Elimina tutte le immagini alternative**: rimuove tutte le versioni di un’immagine, tranne la versione destinata alla visualizzazione sullo schermo. Alcuni PDF includono più versioni della stessa immagine per scopi diversi, come la visualizzazione su schermo a bassa risoluzione e la stampa ad alta risoluzione.
* **Elimina tag documento**: rimuove i tag dal documento, rimuovendo anche le funzionalità di accessibilità e ridisposizione del testo.
* **Rilevare E Unire Frammenti Di Immagini**: cerca le immagini o le maschere frammentate in porzioni sottili e tenta di unire le porzioni in una singola immagine o maschera.
* **Elimina indice di ricerca incorporato**: rimuove gli indici di ricerca incorporati, riducendo le dimensioni del file.

#### Elimina dati utente {#discard-user-data}

Seleziona **Elimina dati utente** per rimuovere le informazioni personali che non si desidera distribuire o condividere con altri utenti.

* **Elimina Tutti I Commenti, Forms E Multimedia**: rimuove tutti i commenti, i moduli, i campi modulo e gli elementi multimediali da PDF.
* **Elimina tutti i dati oggetto**: rimuove tutti gli oggetti dal PDF.
* **Elimina riferimenti incrociati esterni**: rimuove i collegamenti ad altri documenti. I collegamenti che passano ad altre posizioni all’interno del PDF non vengono rimossi.
* **Elimina Il Contenuto Dei Livelli Nascosti E Appiattisci I Livelli Visibili**: riduce le dimensioni del file. Il documento ottimizzato ha l&#39;aspetto del PDF originale ma non contiene informazioni sui livelli.
* **Elimina Informazioni Documento E Metadati**: rimuove le informazioni nel dizionario delle informazioni del documento e tutti i flussi di metadati. Utilizzare il comando Salva con nome per ripristinare i flussi di metadati in una copia del PDF.
* **Elimina allegati**: rimuove tutti gli allegati, inclusi quelli aggiunti al PDF come commenti. (PDF Optimizer non ottimizza i file allegati).
* **Eliminare I Dati Privati Di Altre Applicazioni**: elimina da un documento PDF le informazioni utili solo all&#39;applicazione che ha creato il documento. Questa impostazione non influisce sulla funzionalità del PDF, ma riduce le dimensioni del file.

### Pulisci {#clean-up}

Seleziona **Pulisci** per rimuovere gli elementi non necessari dal documento.
Questi elementi includono elementi obsoleti o non necessari per l&#39;uso previsto del documento. La rimozione di alcuni elementi può compromettere gravemente la funzionalità del PDF. Per impostazione predefinita, vengono selezionati solo gli elementi che non influiscono sulla funzionalità. Se non si è sicuri delle implicazioni della rimozione di altre opzioni, utilizzare le selezioni predefinite.

**Compressione**

Selezionate una delle seguenti opzioni di compressione Flate dal menu a discesa:

* Comprimi intero file
* Comprimi struttura documento
* Rimuovi compressione
* Lascia intatta la compressione

**Usa Flate Per Codificare Flussi Non Codificati**: applica la compressione Flate a tutti i flussi non codificati.

**Ignora segnalibri non validi**: rimuove i segnalibri che puntano alle pagine del documento eliminate.

**Elimina destinazioni denominate senza riferimento**: rimuove dal documento PDF le destinazioni denominate a cui non si fa riferimento internamente. Questa opzione non verifica la presenza di collegamenti da altri file o siti Web di PDF.

**Ottimizzare Le PDF Per Una Visualizzazione Web Rapida**: ristruttura un documento PDF per il download pagina alla volta (byte serving) dai server web.

**Nei Flussi Che Utilizzano La Codifica LZW, Utilizza Flate**: applica la compressione Flate a tutti i flussi di contenuto e alle immagini che utilizzano la codifica LZW.

**Elimina collegamenti non validi**: rimuove i collegamenti che passano a destinazioni non valide.

**Ottimizza contenuto pagina**: converte tutti i caratteri di fine riga in caratteri di spaziatura, migliorando la compressione Flate.

## Impostazioni di Microsoft Excel (solo Windows) {#microsoft-excel-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft Excel. Per istruzioni sull&#39;accesso a queste opzioni, vedere [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

**Prova OpenOffice come convertitore di fallback**: quando questa opzione è selezionata e una conversione con Microsoft Excel ha esito negativo o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, nel file di log viene scritta un&#39;eccezione.

**Estensioni nome file**: specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l&#39;applicazione. Il valore predefinito è `xls,xlsx`. Non includere un punto prima o uno spazio tra le estensioni.

**Crea file conforme a PDF/A-1a**: Forza l’utilizzo dell’impostazione PDF/A-1b:2005 RGB Adobe PDF.

**Aggiungere Segnalibri Ad Adobe PDF**: converte i nomi dei fogli di lavoro di Excel in segnalibri. Questa opzione è selezionata per impostazione predefinita.

**Adatta Foglio Di Lavoro A Una Singola Pagina**: riduce le dimensioni del testo per adattarlo al foglio di lavoro in una singola pagina.

**Converti intera cartella di lavoro**: converte tutti i fogli di lavoro nel file di Excel. Se questa opzione non è selezionata, viene convertita solo la pagina corrente.

**Esegui automaticamente macro**: esegue le macro nel documento di Excel, ad esempio una macro che inserisce l&#39;ora corrente, prima di convertire il documento.

**Converti informazioni documento**: aggiunge le proprietà del documento PDF in base alle informazioni del documento nel file di origine. Ciò include informazioni quali titolo del documento, autore, oggetto e parole chiave.

**Aggiungere Collegamenti Ad Adobe PDF**: converte i collegamenti ipertestuali nel file di origine in collegamenti ipertestuali nel documento di PDF.

**Allega Il File Di Origine Ad Adobe PDF**: quando questa opzione è selezionata, il foglio di calcolo Excel originale viene inserito come allegato all’interno del documento PDF generato.

**Abilitare L’Accessibilità E Reflow Con Adobe PDF Con Tag**: incorpora i tag all’interno del documento PDF per abilitare l’accessibilità e il riversamento.

**Elenco Delle Aggiunte Di Excel Da Caricare**: per impostazione predefinita (per motivi di sicurezza), non vengono eseguiti componenti aggiuntivi di Excel quando un file di Excel viene convertito in PDF. Per consentire l&#39;esecuzione di alcuni componenti aggiuntivi di Excel durante la conversione, fornire un elenco separato da virgole dei nomi dei componenti aggiuntivi.

**Elenco Dei Fogli Di Lavoro Da Convertire**: quando questa casella è vuota, tutti i fogli di lavoro nel foglio di calcolo Excel vengono inclusi nel PDF generato. Per convertire in modo selettivo un sottoinsieme dei fogli di lavoro, fornire un elenco separato da virgole di nomi dei fogli di lavoro.

## Impostazioni di Microsoft PowerPoint (solo Windows) {#microsoft-powerpoint-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft PowerPoint. Per istruzioni sull&#39;accesso a queste opzioni, vedere [Creare o modificare le impostazioni del tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Prova OpenOffice come convertitore di fallback]**: quando questa opzione è selezionata e una conversione con Microsoft PowerPoint non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, nel file di log viene scritta un&#39;eccezione.

**[!UICONTROL Estensioni nome file]**: specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l&#39;applicazione. Il valore predefinito è ppt,pptx. Non includere un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni documento]**: aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, società, categoria e commenti. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Aggiungere Segnalibri Ad Adobe PDF]**: converte i titoli di PowerPoint in segnalibri. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Allega Il File Di Origine Ad Adobe PDF]**: aggiunge il file di origine al file PDF come allegato. Questa opzione è deselezionata per impostazione predefinita.

**[!UICONTROL Abilitare L’Accessibilità E Reflow Con Adobe PDF Con Tag]**: incorpora i tag nel file PDF. Questa opzione è deselezionata per impostazione predefinita.

**[!UICONTROL Converti file multimediali in file multimediali PDF]**: converte contenuti multimediali in PDF multimediali, ove possibile. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Converti note altoparlanti]**: converte le note del relatore in PDF.

**[!UICONTROL Esegui automaticamente macro]**: esegue le macro nel documento di PowerPoint, ad esempio una macro che inserisce l&#39;ora corrente, prima di convertire il documento.

**[!UICONTROL Layout PDF basato sulle impostazioni della stampante PowerPoint]**: utilizza le impostazioni della stampante di PowerPoint per disporre il documento PDF.

**[!UICONTROL Aggiungere Collegamenti Ad Adobe PDF]**: mantiene i collegamenti esistenti quando il file viene convertito. L’aspetto dei collegamenti è generalmente invariato. I collegamenti possono essere creati solo se è selezionata anche l’opzione Abilita accessibilità. Questa opzione è deselezionata per impostazione predefinita.

**[!UICONTROL Salvare Le Transizioni Delle Diapositive In Adobe PDF]**: converte le transizioni delle diapositive. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Salvare Animazioni In Adobe PDF]**: salva le animazioni convertite nel file PDF.

**[!UICONTROL Converti diapositive nascoste in pagine PDF]**: converte le diapositive nascoste.

**[!UICONTROL Crea file conforme a PDF/A-1a]**: Forza l’utilizzo dell’impostazione PDF/A-1b:2005 RGB Adobe PDF. Alcune funzionalità di PowerPoint non vengono convertite quando si genera un file PDF. Se una transizione di PowerPoint non ha una transizione equivalente in Acrobat, viene sostituita una transizione simile. Se più effetti di animazione si trovano nella stessa diapositiva, viene utilizzato un unico effetto. Le transizioni di pagina e i fly-in di punti elenco vengono convertiti.

## Impostazioni progetto Microsoft (solo Windows) {#microsoft-project-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di progetto di Microsoft. Per istruzioni sull&#39;accesso a queste opzioni, vedere [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

1. **[!UICONTROL Estensioni nome file:]** Specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l&#39;applicazione. Il valore predefinito è `mpp`. Non includere un punto prima o uno spazio tra le estensioni.

1. **[!UICONTROL Converti informazioni documento]**: aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, società, categoria e commenti. Questa opzione è selezionata per impostazione predefinita.
1. **[!UICONTROL Allega Il File Di Origine Ad Adobe PDF]**: aggiunge il file di origine al file PDF come allegato.
1. **[!UICONTROL Crea file conforme a PDF/A-1a]**: Forza l’utilizzo dell’impostazione PDF/A-1b:2005 RGB Adobe PDF.
1. **[!UICONTROL Esegui automaticamente macro]**: esegue tutte le macro del documento di Microsoft Project, ad esempio una macro che inserisce l&#39;ora corrente, prima di convertire il documento.

## Impostazioni di Microsoft Word (solo Windows) {#microsoft-word-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft Word. Per istruzioni sull&#39;accesso a queste opzioni, vedere [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

**[!UICONTROL Prova OpenOffice come convertitore di fallback]**: quando questa opzione è selezionata e una conversione con Microsoft Word non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando OpenOffice. Se la conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, nel file di log viene scritta un&#39;eccezione.

**[!UICONTROL Estensioni nome file]**: specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l&#39;applicazione. Il valore predefinito è `doc,docx,rtf,txt`. Non includere un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni documento]**: aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, società, categoria e commenti. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Aggiungere Segnalibri Ad Adobe PDF]**: converte le intestazioni in segnalibri. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Allega Il File Di Origine Ad Adobe PDF]**: aggiunge il file di origine al file PDF come allegato.

**[!UICONTROL Convertire Riferimenti Incrociati E Sommario In Collegamenti]**: converte tutti i riferimenti incrociati e le voci del sommario in collegamenti. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Abilitare L’Accessibilità E Reflow Con Adobe PDF Con Tag]**: incorpora i tag nel file PDF. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Crea file conforme a PDF/A-1a]**: se selezionata, forza l’utilizzo dell’impostazione PDF/A-1b:2005 RGB Adobe PDF.

**[!UICONTROL Esegui automaticamente macro]**: esegue tutte le macro del documento di Word, ad esempio una macro che inserisce l&#39;ora corrente, prima di convertire il documento.

**[!UICONTROL Mantieni markup documento in Adobe PDF]**: converte le annotazioni nel documento di Word in annotazioni nel file PDF.

**[!UICONTROL Aggiungere Collegamenti Ad Adobe PDF]**: converte i collegamenti ipertestuali nel file di origine in collegamenti ipertestuali nel documento di PDF.

**[!UICONTROL Converti Collegamenti Nota A Piè Di Pagina E Nota Di Chiusura]**: crea collegamenti dalle citazioni delle note a piè di pagina e di chiusura alle note del documento di PDF.

**[!UICONTROL Convertire i commenti visualizzati in note in Adobe PDF]**: converte i commenti nel documento di Word in note di testo nel documento di PDF.

**[!UICONTROL Abilita assegnazione tag avanzati]**: aggiunge tag avanzati per migliorare l’accessibilità.

**[!UICONTROL Converti Tutti Gli Stili In Segnalibri]**: converte tutti gli stili del documento di Word in segnalibri nel documento di PDF.

**[!UICONTROL Converti gli stili specificati in segnalibri]**: converte gli stili definiti nella sezione **[!UICONTROL Stili con livelli]** ai segnalibri nel documento PDF.

**[!UICONTROL Stili con livelli]**: specifica quali stili del documento di Word vengono convertiti in segnalibri nel documento di PDF. Specifica inoltre il livello dei segnalibri. Per utilizzare questa funzione, deseleziona la **[!UICONTROL Converti Tutti Gli Stili In Segnalibri]** e specificare i nomi degli stili nel seguente formato:

**styleName1=level1[,styleName2=level2...]**

Se un nome di stile di Microsoft Word include una virgola (,) o un segno di uguale (=), anteporre ai caratteri speciali il carattere di escape (&quot;\_). Ad esempio, specifica uno stile denominato &quot;Titolo, 1&quot; come Titolo\, 1.

**Codifica Acrobat PDFMaker:** Specifica il tipo di codifica dei file di testo normale di input per Acrobat PDFMaker. Ad esempio, se utilizzi un file codificato UTF-8, seleziona UTF-8 per ottenere risultati ottimali.

## Impostazioni di Microsoft Visio (solo Windows) {#visio}

**Converti informazioni documento**: aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, società, categoria e commenti. Questa opzione è selezionata per impostazione predefinita. Questa opzione è attivata per impostazione predefinita.

**Aggiungere Collegamenti Ad Adobe PDF**: mantiene tutti i collegamenti. Questa opzione è selezionata per impostazione predefinita.

**Aggiungere Segnalibri Ad Adobe PDF**: converte le intestazioni in segnalibri. Questa opzione è selezionata per impostazione predefinita.

**Allega Il File Di Origine Ad Adobe PDF**: aggiunge il file di origine al file PDF come allegato.

**Livelli Sempre Piatti In Adobe PDF**: Appiattisce tutti i livelli di Visio.

**Converti tutte le pagine**: converte tutte le pagine del file di Visio.

**Apri Il Pannello Livelli In Adobe Acrobat**: se i livelli di Visio non vengono appiattiti, apre una finestra in cui è possibile specificare i livelli che vengono conservati nel file PDF quando vengono aperti con Acrobat. Questa opzione è selezionata per impostazione predefinita.

**Crea file conforme a PDF/A-1b**: Forza l’utilizzo di Adobe PDF Setting PDF/A-1b:2005 (RGB).

**Convertire Commenti In Commenti Adobe PDF**: converte le note di Visio in commenti di PDF.

## Impostazioni di Microsoft Publisher (solo Windows) {#microsoft-publisher-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file di Microsoft Publisher. Per istruzioni sull&#39;accesso a queste opzioni, vedere [Creare o modificare le impostazioni del tipo di file](#create-or-edit-file-type-settings).

**[!UICONTROL Estensioni nome file]**: specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l&#39;applicazione. Il valore predefinito è `pub`. Non includere un punto prima o uno spazio tra le estensioni.

## Impostazioni AutoCAD (solo Windows) {#autocad-settings-windows-only}

Queste opzioni determinano la modalità di conversione dei file AutoCAD. Per istruzioni sull&#39;accesso a queste opzioni, vedere [Creare o modificare le impostazioni del tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Estensioni nome file]**: specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per l&#39;applicazione. Il valore predefinito è `dwg`. Non includere un punto prima o uno spazio tra le estensioni.

**[!UICONTROL Converti informazioni documento]**: aggiunge informazioni sul documento dalla finestra di dialogo Proprietà del file di origine, inclusi titolo, oggetto, autore, parole chiave, manager, società, categoria e commenti. Questa opzione è selezionata per impostazione predefinita.

**[!UICONTROL Aggiungere Segnalibri Ad Adobe PDF]**: converte le intestazioni in segnalibri.

**[!UICONTROL Livelli Sempre Piatti In Adobe PDF]**: appiattisce tutti i livelli AutoCAD.

**[!UICONTROL Apri Il Riquadro Livelli In Adobe Acrobat]**: mostra la struttura dei livelli quando il PDF viene aperto in Acrobat.

**[!UICONTROL Converti tutti i layout]**: include tutti i layout nel PDF.

**[!UICONTROL Converti spazio modello in 3D]**: se selezionata, il layout dello spazio modello viene convertito in un’annotazione 3D in PDF.

**[!UICONTROL Aggiungere Collegamenti Ad Adobe PDF]**: se selezionata, mantiene tutti i collegamenti.

**[!UICONTROL Allega Il File Di Origine Ad Adobe PDF]**: aggiunge il file di origine al file PDF come allegato.

**[!UICONTROL Crea file conforme a PDF/A-1b]**: Forza l’utilizzo dell’impostazione Adobe PDF PDF/A-1b.

**[!UICONTROL Converti tutti i livelli]**: per default, PDF Generator converte solo il livello di default dei file AutoCAD in PDF anziché tutti i livelli all&#39;interno del file. Selezionate questa opzione per convertire tutti i livelli del file.

**[!UICONTROL Incorpora informazioni scala]**: mantiene le informazioni sulla scala del disegno.

**[!UICONTROL Converti layout corrente]**: include solo il layout corrente nel PDF.

**[!UICONTROL Elenco dei layout AutoCAD da convertire]**: un disegno AutoCAD può avere più layout. Se questa casella è vuota, tutti i layout del disegno AutoCAD vengono inclusi nel documento PDF generato. Per convertire selettivamente un sottoinsieme dei layout, fornisci un elenco separato da virgole di nomi di layout.

## Impostazioni di OpenOffice {#openoffice-settings}

Queste opzioni determinano la modalità di conversione dei file di OpenOffice. Per istruzioni sull&#39;accesso a queste opzioni, vedere [Creare o modificare le impostazioni del tipo di file](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Prova PDFMaker come fallback Converter**: quando questa opzione è selezionata e una conversione tramite OpenOffice non riesce o raggiunge il limite di timeout specificato, PDF Generator tenta la conversione utilizzando PDFMaker. Se la conversione tramite PDFMaker non riesce o raggiunge il limite di timeout specificato, nel file di registro viene scritta un&#39;eccezione.

**Estensioni nome file**: specifica le estensioni del nome file per i tipi di file, separati da virgole, accettati per questa applicazione. Il valore predefinito è `odt,odp,ods,odg,odf,sxw,sxi,sxd`. Non includere un punto prima o uno spazio tra le estensioni.

**Intervallo**: converte tutte le pagine o specifica pagine particolari o un intervallo di pagine. Se non è definito alcun intervallo di pagine, vengono convertite tutte le pagine. Per esportare un intervallo di pagine, utilizza il formato 3-6. Per esportare pagine singole, utilizzare il formato 7;9;11. È possibile esportare una combinazione di intervalli di pagine e pagine singole utilizzando un formato come 3-6;8;10;12.

**Orientamento pagina**: solo per i file di testo normale, selezionare Verticale o Orizzontale per il documento PDF convertito.

**Immagini**: configura la modalità di conversione delle immagini. Le immagini EPS con anteprime incorporate vengono esportate solo come anteprime. Le immagini EPS senza anteprime incorporate vengono esportate come segnaposto vuoti. Con la compressione delle immagini senza perdita di dati, tutti i pixel vengono mantenuti. Con la compressione JPEG delle immagini e un livello di qualità elevato, vengono mantenuti quasi tutti i pixel. Con un livello di qualità basso, alcuni pixel si perdono e vengono introdotti artefatti, ma le dimensioni dei file si riducono.

**Generale**: abilita le opzioni per convertire un PDF con tag o esportare le note dei documenti Writer e FormCalc, gli effetti di transizione delle diapositive Impress o le pagine vuote in PDF. Quando si esportano i tag, la dimensione del file può aumentare in modo significativo. Alcuni tag esportati sono sommari, collegamenti ipertestuali e controlli.

È inoltre possibile specificare la modalità di invio dei moduli. Le opzioni sono XML, FDF, PDF o HTML. Questa impostazione sostituisce la proprietà URL del controllo impostata nel documento. Per il documento PDF può essere selezionata una sola impostazione comune:

* PDF (invia l&#39;intero documento)
* DFF (invia il contenuto del controllo)
* HTML
* XML

**PDF con tag**: consente la creazione di PDF con tag da documenti OpenOffice. PDF con tag contiene informazioni sulla struttura del contenuto del documento. Questo può essere utile quando il documento viene visualizzato su dispositivi con schermi diversi e quando si utilizza un software per la lettura dello schermo. Consente inoltre al software di accesso facilitato di eseguire varie operazioni utili con il documento di PDF, ad esempio la lettura ad alta voce del contenuto del documento di PDF.

**Esporta note**: converte le note nei documenti OpenOffice in note nel documento PDF generato.

**Usa effetti di transizione**: converte gli effetti di transizione delle diapositive nelle presentazioni di OpenOffice negli effetti di transizione PDF corrispondenti.

**Invia Forms In Formato**: crea un modulo PDF che può essere compilato e stampato dall’utente del documento PDF.

**Esporta pagine vuote inserite automaticamente**: quando questa opzione è selezionata, le pagine vuote inserite automaticamente vengono incluse nel documento PDF generato. Questa opzione è utile se si stampa un documento PDF su due lati. Ad esempio, un libro può essere configurato in modo che la prima pagina del capitolo inizi sempre su una pagina con numero dispari. Se il capitolo precedente termina su una pagina con numero dispari, OpenOffice inserisce una pagina vuota con numero pari. Questa opzione controlla se includere la pagina con numero pari nel PDF generato.

## Altre impostazioni dell&#39;applicazione (solo Windows) {#other-applications-settings-windows-only}

Non è possibile modificare le impostazioni per altre applicazioni tramite la console di amministrazione, poiché visualizzano le estensioni dei nomi di file per i tipi di file supportati. Per istruzioni sull&#39;accesso a queste impostazioni, vedere [Creare o modificare le impostazioni del tipo di file](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* PageMaker Adobe: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

Potrebbe essere necessario personalizzare il supporto per questi tipi di file. Per ulteriori informazioni, consulta &quot;Aggiunta di supporto per formati di file nativi aggiuntivi&quot; in [Programmazione con i moduli AEM](https://www.adobe.com/go/learn_aemforms_programming_62).

Per informazioni sulla configurazione di una stampante di rete PDFG, vedere [Configurazione di una stampante di rete PDFG (solo Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
