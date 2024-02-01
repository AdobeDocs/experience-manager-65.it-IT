---
title: Utilizzo di grafici in un modulo adattivo.
description: Utilizza i grafici in un modulo adattivo per rendere il modulo più informativo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Adaptive Forms, Foundation Components
source-git-commit: 5c117d25a381b2cb85c2bf0715866dd5ad93572c
workflow-type: tm+mt
source-wordcount: '2001'
ht-degree: 0%

---

# Grafici moduli adattivi {#af-charts}

![Immagine_protagonista](assets/charts_hero_image.jpg)

Un grafico o un grafico è una rappresentazione visiva dei dati. Consente di condensare grandi quantità di informazioni in un formato visivo e di facile comprensione, consentendo di visualizzare, interpretare e analizzare in modo migliore dati complessi.
Il pacchetto di componenti aggiuntivi per AEM Forms fornisce un componente grafico pronto all’uso. Puoi utilizzare nei moduli e nei documenti adattivi per la rappresentazione visiva di dati bidimensionali in pannelli e tabelle ripetibili. Il componente Grafico consente di aggiungere e configurare i seguenti tipi di grafici:

1. Torta
1. Colonna
1. Anello
1. Barra
1. Linea
1. Linea e punto
1. Punto
1. Area

Il componente Grafico supporta e fornisce funzioni statistiche incorporate - somma, media, massimo, minimo, modalità, mediana, intervallo e frequenza - per calcolare e tracciare i valori su un grafico. Oltre alle funzioni pronte all’uso, puoi scrivere funzioni personalizzate e renderle disponibili per l’utilizzo nei grafici.

Vediamo ora come aggiungere e configurare il componente Grafico:

## Aggiungi grafico {#add-chart}

Per impostazione predefinita, il componente Grafico è disponibile nella barra laterale dell’AEM. In modalità di authoring, puoi trascinare il componente Grafico dalla barra laterale AEM al modulo o al documento adattivo. Quando rilasci il componente, questo crea un segnaposto per un grafico.

## Configura grafico {#configure-chart}

>[!NOTE]
> 
> Prima di configurare il grafico, accertati che il pannello o la riga di tabella per cui stai configurando il grafico sia impostato su ripetibile. Nella scheda Impostazioni ripetizione della finestra di dialogo Modifica componente è possibile specificare il conteggio minimo e massimo per la riga ripetibile del pannello o della tabella.

Per configurare il grafico, fare clic con il pulsante destro del mouse sul componente Grafico e scegliere Modifica per aprire la finestra di dialogo Modifica grafico. La finestra di dialogo include le schede Titolo e testo, Configurazione, Opzioni avanzate e Stile, che consentono di configurare il grafico.

### Base {#basic}

Nella scheda Base, puoi configurare le seguenti proprietà:

![Proprietà grafico](assets/chart-properties.png)

* **Nome elemento**: identificatore dell’elemento grafico nella struttura del contenuto JCR. Non è visibile nel grafico, ma è utile quando si fa riferimento all’elemento da altri componenti, script ed espressioni SOM.
* **Tipo di grafico**: specifica il tipo di grafico che si desidera generare. Le opzioni disponibili sono Torta, Anello, Barra, Colonna, Linea, Linea e Punto, Punto e Area. Nell&#39;esempio, il tipo di grafico è Colonna.
* **Nome Riga Ripetuto Per Origine Dati**: specifica il nome dell’elemento della riga della tabella o del pannello ripetibile da cui verranno originati i dati. Nell&#39;esempio, statementDetails è il nome dell&#39;elemento della riga ripetibile nella tabella Statement Details.
* **Asse X > Titolo**: specifica il titolo dell&#39;asse X. Nell&#39;esempio, il titolo dell&#39;asse X è Categoria.
* **Asse X > Campo**: specifica il nome dell&#39;elemento del campo (o di una cella in una tabella) da tracciare sull&#39;asse X. Nell’esempio, le categorie sono configurate sull’asse X. Il nome dell&#39;elemento per la cella della tabella nella colonna Categoria della tabella di esempio è categoria.
* **Asse X > Usa funzione**: specifica la funzione statistica da utilizzare per calcolare i valori sull’asse X. Nell’esempio, l’opzione selezionata è Nessuno. Per ulteriori informazioni sulle funzioni, vedere Utilizzare le funzioni nel grafico.
* **Asse Y > Titolo**: specifica il titolo dell&#39;asse Y. Nell&#39;esempio, il titolo dell&#39;asse Y è Spesa.
* **Asse Y > Campo**: specifica il nome dell&#39;elemento del campo (o della cella in una tabella) da tracciare sull&#39;asse Y. Nell’esempio, configura la quantità sull’asse Y. Il nome dell&#39;elemento per la cella della tabella nella colonna Importo della tabella di esempio è importo.
* **Asse Y > Usa funzione**: specifica la funzione statistica da utilizzare per calcolare i valori sull’asse Y. Nell’esempio, viene aggiunto l’importo speso in ciascuna categoria e il valore calcolato viene tracciato sull’asse Y. Pertanto, selezionare Somma dall&#39;elenco a discesa Usa funzione. Per ulteriori informazioni sulle funzioni, vedere Utilizzare le funzioni nel grafico.
* **Posizione legenda**: specifica la posizione della legenda rispetto al grafico. Le opzioni disponibili sono Right, Left, Top e Bottom.
* **Mostra legenda**: se selezionata, mostra una legenda per il grafico.
* **Descrizione**: specifica il formato in cui la descrizione comando viene visualizzata al passaggio del mouse su una coordinata nel grafico. Il valore predefinito è **\${x}(\${y})**. A seconda del tipo di grafico, quando si posiziona il mouse su un punto, una barra o una sezione del grafico, le variabili **\${x}** e **\${y}** vengono sostituite dinamicamente con i valori corrispondenti sull&#39;asse X e sull&#39;asse Y e visualizzate nella descrizione comando. Come mostrato nell&#39;esempio seguente, la descrizione viene visualizzata come **Negozi al dettaglio(5870)** quando si punta il mouse sulla colonna Retail Stores (Negozi al dettaglio). Per disattivare la descrizione, lasciare vuoto il campo Descrizione. Questa opzione non è applicabile ai grafici a linee e a superficie.
* **Configurazioni specifiche per il grafico**: oltre alle configurazioni comuni, è disponibile la seguente configurazione specifica per il grafico:
* **Raggio interno**: disponibile per i grafici ad anello per specificare il raggio (in pixel) del cerchio interno del grafico.
* **Colore linea**: disponibile per i grafici a linee, a linee, a punti e ad area per specificare il valore esadecimale del colore della linea nel grafico.
* **Colore punto**: disponibile per i grafici Punto e Linea e Punto per specificare il valore esadecimale del colore per i punti del grafico.
* **Colore area**: disponibile per i grafici a superficie per specificare il valore esadecimale del colore per l’area sotto la linea del grafico.
* **Classe CSS**: specifica il nome di una classe CSS nel campo della classe CSS per applicare al grafico uno stile personalizzato.

### Configurazione {#configuration}

Nella scheda Base è possibile definire il tipo di grafico, il pannello di origine o la riga della tabella che contiene i dati, i valori da tracciare sull&#39;asse X e sull&#39;asse Y del grafico e, facoltativamente, la funzione statistica per calcolare i valori da tracciare sul grafico.

Comprendiamo in dettaglio le informazioni contenute in questa scheda, con l’aiuto di un esempio di tabella ripetibile nell’estratto conto di una carta di credito. Si supponga di voler generare un grafico per rappresentare e correlare le spese totali in diverse categorie nella sezione dei dettagli rendiconto di un rendiconto della carta di credito, come illustrato di seguito.

A questo scopo, è necessario tracciare le categorie sull&#39;asse X e, sull&#39;asse Y, tracciare la spesa totale in ciascuna categoria.

![Dettagli rendiconto](assets/statement-details.png)

L’estratto conto della carta di credito utilizzato in questo esempio è un documento adattivo e la sezione dei dettagli dell’estratto conto è una tabella che si presenta come segue nella modalità di creazione.

![Authoring dei dettagli dell’istruzione](assets/statement-details-authoring.png)

Consideriamo i seguenti requisiti e condizioni per la generazione del grafico:

* Nel grafico viene visualizzata la spesa totale in ciascuna categoria della tabella Dettagli rendiconto.
* Il tipo di grafico è Colonna, anche se è possibile scegliere qualsiasi altro tipo di grafico, a seconda delle necessità.
* La riga Tabella nella tabella Dettagli istruzione è ripetibile. Puoi configurarlo nel campo Impostazioni ripetizione delle proprietà della riga della tabella.
* Il nome dell&#39;elemento per la riga è statementDetails. Puoi configurarlo nelle proprietà della riga di tabella.
* Il nome dell&#39;elemento per la cella della tabella nella colonna Categoria è categoria. Puoi specificarlo in linea. Seleziona la cella e tocca il pulsante Modifica.
* Il nome dell&#39;elemento per la cella della tabella nella colonna Importo è importo. Inoltre, la cella della tabella nella colonna Importo è una casella numerica.
* Con la configurazione specificata, l&#39;istogramma nell&#39;esempio verrà visualizzato come segue. Ogni colore rappresenta una categoria e nel grafico vengono sommati i singoli elementi o importi di una categoria.

  ![Grafico](assets/chart.png)

La legenda e la punta dell&#39;utensile vengono visualizzate nel modo seguente.

![Descrizione comando legenda grafico](assets/chart-legend-tooltip.png)

### Attribuzione stile {#styling}

In modalità Stile è possibile configurare la larghezza, in percentuale della larghezza totale disponibile nel modulo o nel documento, e l&#39;altezza, in pixel, per il grafico. Altre opzioni includono testo, sfondo, bordo, effetti e sostituzioni CSS.

Per passare alla modalità stile, nella barra degli strumenti della pagina: **tocca>>Stile**.

![Proprietà del grafico disponibili per lo stile](assets/chart-styling.png)

## Utilizzare le funzioni nel grafico {#use-functions}

È possibile configurare un grafico in modo da utilizzare le funzioni statistiche per calcolare i valori dai dati di origine per il plottaggio sul grafico. Il componente Grafico include alcune funzioni incorporate, ma puoi scriverle e renderle disponibili per l’utilizzo nella configurazione del grafico.

>[!NOTE]
>
> È possibile utilizzare le funzioni per calcolare i valori dell&#39;asse X o dell&#39;asse Y in un grafico.

### Funzioni predefinite {#default-functions}

Per impostazione predefinita, con il componente Grafico sono disponibili le seguenti funzioni:

* **Media (media)**: restituisce la media dei valori sull’asse X o Y per un determinato valore sull’altro asse.
* **Somma**: restituisce la somma di tutti i valori sull’asse X o Y per un determinato valore sull’altro asse.
* **Massimo**: restituisce il massimo dei valori sull’asse X o Y per un determinato valore sull’altro asse.
* **Frequenza**: restituisce il numero di valori sull’asse X o Y per un determinato valore sull’altro asse.
* **Intervallo**: restituisce la differenza tra il valore massimo e il valore minimo sull’asse X o Y per un determinato valore sull’altro asse.
* **Mediana**: restituisce il valore che separa i valori più alti e più bassi a metà sull’asse X o Y per un determinato valore sull’altro asse.
* **Minimo**: restituisce il minimo dei valori sull’asse X o Y per un determinato valore sull’altro asse.
* **Modalità**: restituisce il valore con la maggior parte delle occorrenze sull’asse X o Y per un determinato valore sull’altro asse

### Funzioni personalizzate {#custom-functions}

Oltre a utilizzare le funzioni predefinite nei grafici, è possibile scrivere funzioni personalizzate in JavaScript e renderle disponibili nell’elenco delle funzioni nel componente Grafico.

Una funzione accetta una matrice o più valori e un nome di categoria come input e restituisce un valore. Ad esempio:

```
Multiply(valueArray, category) {
    var val = 1;
    _.each(valueArray, function(value) {
        val = val * value;
    });
    return val;
}
```

Dopo aver scritto una funzione personalizzata, eseguire le operazioni seguenti per renderla disponibile per l&#39;utilizzo nella configurazione del grafico:

1. Aggiungi la funzione personalizzata nella libreria client associata al modulo o al documento adattivo.
1. In CRXDE Liti, crea un nodo nt:unstructured nella cartella delle app con le seguenti proprietà:
   * Impostare guideComponentType su fd/af/reducer. (obbligatorio)
   * Imposta il valore su un nome completo della funzione JavaScript personalizzata. (obbligatorio)
   * Impostare jcr:description su un nome significativo. Viene visualizzato nel **Usa funzione** elenco a discesa. Ad esempio: **Moltiplica**.
   * Impostare qtip su una breve descrizione della funzione. Viene visualizzata come descrizione quando si passa il puntatore sul nome della funzione nell&#39;elenco a discesa Usa funzione.
   * Clic **Salva tutto** per salvare la configurazione.
   * La funzione è ora disponibile per l’utilizzo nel grafico.

![Funzione personalizzata](assets/custom-function.png)


## Aggiorna grafico automaticamente {#auto-refresh-chart}

Un grafico viene aggiornato automaticamente quando gli utenti eseguono una delle operazioni seguenti:
* Aggiunge o rimuove un&#39;istanza del pannello dell&#39;origine dati o della riga di tabella.
* Modificate qualsiasi valore tracciato sull&#39;asse X o Y nel pannello dell&#39;origine dati o nella riga della tabella.
* Modificare il tipo di grafico.

## Utilizza il tipo di grafico nelle regole dei moduli adattivi {#chart-in-rules}

La proprietà chartType specifica il tipo di grafico. I valori possibili sono torta, ciambella, barra, linea, punto di linea, punto e area. Si tratta di una proprietà scrivibile, che consente di utilizzarla in [regole per moduli adattivi](/help/forms/using/rule-editor.md) per manipolare le configurazioni dei grafici. Comprendiamolo con l&#39;aiuto di un esempio.

Considera di aver configurato un istogramma. Si desidera tuttavia anche fornire agli utenti un&#39;opzione per selezionare un tipo di grafico diverso da un elenco a discesa e ridisegnare il grafico. È possibile ottenere questo risultato utilizzando la proprietà chartType in una regola nel modo seguente:

1. Trascina un componente elenco a discesa dalla barra laterale AEM nel modulo adattivo.
1. Seleziona il componente e tocca ![Impostazioni](cmppr1.png).
1. Specifica un titolo per l’elenco a discesa. Selezionare ad esempio il tipo di grafico.
1. Aggiungi i tipi di grafico supportati nella sezione Elementi, per popolare l’elenco a discesa. Clic **Fine**.
   ![Selezione dell’elenco a discesa del grafico](chart-drop-down.png)

1. Seleziona il componente a discesa e tocca ![Testo alternativo](rule_editor_icon.png). Nell’editor delle regole, scrivi una regola nell’editor delle regole visive come mostrato di seguito.
   ![Impostazione delle regole del grafico](assets/chart-rules.png)

   In questo esempio, il nome dell’elemento del componente grafico è **grafico personale**.

   In alternativa, puoi scrivere le seguenti regole nell’editor di codice.

   ![Regole del grafico](assets/chart-code-rule.png)

   Per ulteriori informazioni sulla scrittura delle regole, consulta [Editor regole](/help/forms/using/rule-editor.md)

1. Fai clic su Fine per salvare la regola.

È ora possibile selezionare un tipo di grafico dall&#39;elenco a discesa e fare clic su aggiorna per ridisegnare il grafico.


