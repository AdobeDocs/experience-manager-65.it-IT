---
title: La generazione di PDF non riesce a stampare un numero elevato di PDF con WorkBench
description: Quando un cliente genera un numero elevato di PDF tramite servizi implementati tramite WorkBench, il servizio di stampa non riesce.
exl-id: f3746b8e-4c38-447a-b5bf-d11fc77556f7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Troubleshooting
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# La generazione di PDF non riesce a stampare un numero elevato di PDF tramite WorkBench {#PDF-generation-fails-to-print-a-large-number-of-PDFs-via-WorkBench}

## Problema   {#issue}

Quando un cliente genera un numero elevato di PDF tramite servizi implementati tramite WorkBench. Errore del servizio a causa di memoria insufficiente. L’errore viene visualizzato come:

`ALC-OUT-002-013: XMLFormFactory, PAexecute failure: "0: Out of Memory"`

<!-- Attached is a simplified template (BollatoRiservatiLandscape_table_simple.xdp) that simulates the problem.
Using the Designer, if we associate the template "BollatoRiservatiLandscape_table_semplice.xdp" with the XML file "BollatoRiservati.xml" during the generation of the pdf, the process comes to occupy 1.6 Gb of RAM. On the server side, with the complete template, the pdf generation process breaks down, occupying 2 GB of RAM.-->

Questo perché il numero massimo di pagine in una richiesta di stampa è limitato a circa 1000 pagine su Windows. Quando si genera un output di stampa, il modello e i dati devono essere caricati in memoria e il layout risultante deve essere incorporato nella memoria. Ciò significa che esistono limiti alla dimensione dell’output finale. Il processo che genera l&#39;output di stampa è un&#39;attività a 32 bit, il che significa che è limitato a 2 GB di RAM su Windows <!--and 4 GB on UNIX-->.

## Applicabile a {#applies-to}

La soluzione si applica ad AEM Forms <!--JEE Server and AEM Forms on OSGi Server--> per x86_win32 XMLFM.

## Soluzione {#solution}

Il fattore più importante che influisce sull’utilizzo della memoria è la quantità di dati presenti in un modulo. Tuttavia, in una progettazione di moduli sono presenti altri fattori che influiscono in misura minore sull&#39;utilizzo della memoria. Tenendo conto di questi fattori, è possibile progettare un modulo per un output di stampa più grande. La sezione seguente indica, in ordine di priorità, i fattori che influenzano l’ingombro della memoria:

### Fattore di impatto {#impact-factor}

**Alta**

1. **Sottomaschere di scelta** - Un set di sottomaschere di scelta è una variante dell&#39;oggetto set di sottomaschere che consente di personalizzare la visualizzazione di sottomaschere specifiche dall&#39;interno del set utilizzando le istruzioni condizionali.
1. **Usa testo statico al posto dei sottotitoli** : quasi tutti i campi forniscono una didascalia all’interno di, l’utente dovrebbe utilizzarla invece di utilizzare come didascalia un testo statico aggiuntivo.
1. Utilizzare **Formato RTF (Rich Text Format)** ove possibile.

**Media**

Altri fattori da considerare durante la progettazione del modello di modulo per migliorare l&#39;utilizzo della memoria:

1. Evita di utilizzare il testo statico per etichettare un campo. Utilizzare invece i sottotitoli nel campo di testo.
2. Non utilizzare in modo eccessivo rettangoli, linee, oggetti e tabelle.
3. Se possibile, evita di utilizzare i sottomoduli Rich Text e Choice.
4. Evitare l&#39;uso eccessivo di sottomaschere e sottomaschere nidificate.

### Limitazione dimensioni dati {#data-size-limitations}

Poiché la memoria massima del processo è limitata e la memoria utilizzata dal processo non dipende solo dalle dimensioni del file di dati. È strettamente collegata alla struttura del modulo e, in una certa misura, alla quantità effettiva di dati incorporati nel modulo.

Se il modulo ha molti nodi di piccole dimensioni con dati di piccole dimensioni, il processo consuma più memoria (e quindi esaurisce la memoria più rapidamente) rispetto a un modulo che ha un numero inferiore di nodi (anche) con dati di grandi dimensioni.

Leggi le [Appendice sotto](#appendix) per ulteriori informazioni, dove i risultati dei test si basano su Stampa modulo (PDF non taggato). L&#39;utilizzo di PDF con tag aumenta i requisiti di memoria del processo. Dipende anche dal numero di campi nel modulo: il requisito di memoria del processo è leggermente superiore a 1,5 volte rispetto a quello di PDF non taggato.

### Forms interattivo {#interactive-forms}

I moduli interattivi consumerebbero più memoria rispetto a Print Forms, in quanto i campi interattivi vengono di nuovo sottoposti a rendering. Nei test effettuati, il consumo di memoria è aumentato di circa 1,5 volte rispetto ai moduli di stampa e si tratta di moduli interattivi statici.

### Formati immagine {#image-formats}

L’Adobe non consiglia alcun formato immagine specifico. Ma sarebbe bello avere un&#39;immagine più piccola, ad es. PNG (Portable Network Graphics). Inoltre non è consigliabile utilizzare immagini ad alta risoluzione le cui dimensioni variano diverse centinaia di MegaByte. Inoltre, non è consigliabile utilizzare immagini compresse le cui dimensioni al momento della decompressione si espandono a diverse centinaia di megabyte di dati.

### Appendice {#appendix}

**Esempi di tabella**

Di seguito sono mostrate diverse varianti di tabelle che mostrano il numero di pagine con rendering rispetto alla dimensione dei dati per le tabelle semplici e complesse.

1. Tabella con una singola colonna in cui vengono generate 5000 pagine di PDF, con dimensioni del file di dati di 24 MB e record a 30 KB.

   ![table_single_column](/help/forms/using/assets/table_single_column.png)

1. Una tabella con molte colonne di piccole dimensioni in cui vengono generate 800 pagine di PDF, le dimensioni del file di dati sono di 4,6 MB e 20 KB.
   ![table_many_small_columns](/help/forms/using/assets/table_many_small_columns.png)

1. Tabella con molte colonne di piccole dimensioni, ma file di dati di dimensioni maggiori a causa dell&#39;utilizzo di nomi xmlTag di dimensioni maggiori.
In questo caso, tutto è uguale a quello precedente, ma i nomi dei tag xml sono stati resi di grandi dimensioni (in modo che le dimensioni del file di dati aumentino senza alcun aumento dei dati effettivi), il risultato finale (limite superiore) è quasi lo stesso. Anche se la dimensione del file di dati è aumentata da 4,6 MB a 44,6 MB. In questo caso vengono generate 800 pagine di PDF, con una dimensione del file di dati di 44,6 MB e record di 20 KB.

   ![table_large_xml_tagname](/help/forms/using/assets/table_bigger_xml_tagname.png)

Pertanto, è difficile impostare un limite massimo generale per la dimensione del file di dati. Ogni modulo è univoco e quindi il consumo di memoria varia da modulo a modulo.
