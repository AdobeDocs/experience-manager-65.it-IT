---
title: Utilizzo dei grafici in Interactive Communications
seo-title: Componente grafico in Interactive Communications
description: Utilizzando i grafici in una comunicazione interattiva, è possibile condensare grandi quantità di informazioni in un formato visivo facile da analizzare
seo-description: ' AEM Forms fornisce un componente grafico che consente di creare grafici nella comunicazione interattiva. Questo documento descrive le configurazioni di base e di agente del componente grafico.'
uuid: 978aa431-9a5b-4964-b37c-7bfa8c3f49b9
content-type: reference
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e21714ad-d445-4aff-b0db-d577061e0907
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2646'
ht-degree: 2%

---


# Utilizzo di grafici in Interactive Communications{#using-charts-in-interactive-communications}

Un grafico o un grafico è una rappresentazione visiva dei dati. Condensa grandi quantità di informazioni in formato visivo facile da capire, consentendo ai destinatari della comunicazione interattiva di visualizzare, interpretare e analizzare meglio i dati complessi.

Durante la creazione di una comunicazione interattiva, è possibile aggiungere grafici per rappresentare visivamente dati bidimensionali dal modello dati del modulo di comunicazione interattiva. Il componente Grafico consente di aggiungere e configurare i seguenti tipi di grafici: Torta, Colonna, Anello, Barre, Linea, Linea e Punto, Punto, Area e Quadrante.

## Aggiungere e configurare il grafico in una comunicazione interattiva {#add-and-configure-chart-in-an-interactive-communication}

Per aggiungere e configurare un grafico in una comunicazione interattiva, effettuate le seguenti operazioni:

1. Toccate **Componenti** dalla barra laterale della comunicazione interattiva.
1. Trascinare il componente **Chart** su uno dei seguenti componenti:

   * Canale di stampa: Area di destinazione o campo immagine
   * Canale Web: Area Pannello o Target

1. Toccate il componente grafico nell&#39;editor delle comunicazioni interattive e selezionate **[!UICONTROL Configura (]** ![configura_icon](assets/configure_icon.png)) dalla barra degli strumenti del componente.

   Le proprietà del grafico vengono visualizzate nel riquadro a sinistra.

   ![Proprietà di base di un grafico del tipo di linea nel canale di stampa](assets/chart_properties_print_new.png)

   Proprietà di base di un grafico del tipo di linea nel canale di stampa

   ![Proprietà di base di un grafico del tipo di linea nel canale Web](assets/chart_properties_web_new.png)

   Proprietà di base di un grafico del tipo di linea nel canale Web

1. Configurare le proprietà [del grafico](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties) in base al tipo di canale.
1. (Solo canale di stampa) In **[!UICONTROL Impostazioni agente]**, specificare se l&#39;utilizzo di questo grafico è obbligatorio per l&#39;agente. Se l&#39;opzione i **[!UICONTROL t è obbligatoria per l&#39;agente per utilizzare questo grafico]** non è selezionata, l&#39;agente può toccare l&#39;icona occhio per il grafico nella scheda **[!UICONTROL Content]** dell&#39;interfaccia utente dell&#39;agente per mostrare o nascondere il grafico.

   ![chart_agentproperties](assets/chart_agentproperties.png)

1. Toccate ![done_icon](assets/done_icon.png) per salvare le proprietà del grafico.

   Toccate **[!UICONTROL Anteprima]** per visualizzare l&#39;aspetto e i dati associati al grafico. Toccate **[!UICONTROL Modifica]** per riconfigurare le proprietà del grafico.

## Configurare le proprietà del grafico {#configure-chart-properties}

Configura le seguenti proprietà durante la creazione di grafici per la stampa e i canali Web:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descrizione</td>
   <td>Tipo canale</td>
  </tr>
  <tr>
   <td>Nome</td>
   <td>Identificatore per l’elemento grafico. Il nome del grafico specificato in questo campo non è visibile nel grafico. Viene utilizzato per fare riferimento all'elemento di altri componenti, script ed espressioni SOM.</td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Tipo di grafico</td>
   <td>Tipo di grafico da generare. Le opzioni disponibili sono Torta, Colonna, Anello, Barre, Linea, Linea e Punto, Punto e Area.</td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Serie &gt; Serie multiple</td>
   <td>Selezionare questa opzione per aggiungere più serie agli elementi della raccolta dei dati del modulo tracciati sull'asse X e sull'asse Y.</td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Serie &gt; Oggetto modello dati</td>
   <td>Nome dell'elemento di raccolta dati del modulo per aggiungere più serie al grafico.<br /> Scegliere una proprietà dell'oggetto modello dati modulo padre per le proprietà tracciate sull'asse X e sull'asse Y per creare una serie significativa. L'oggetto del modello dati associato deve essere di tipo Numero, Stringa o Data.</td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Mostra impilati</td>
   <td>Scegli di impilare i valori di ciascuna serie uno sopra l'altro.</td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Asse X &gt; Titolo</td>
   <td>Titolo per l’asse X.</td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Asse X &gt; Oggetto modello dati</td>
   <td><p>Nome dell'elemento di raccolta dati del modulo da tracciare sull'asse X.</p> <p>Scegliere due proprietà di tipo raccolta/array dello stesso oggetto del modello dati padre che abbiano un significato in relazione l'una all'altra per eseguire il grafico sull'asse X e Y di un grafico. L'oggetto del modello dati associato deve essere di tipo Numero, Stringa o Data.</p> </td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Asse Y &gt; Titolo</td>
   <td>Titolo per l’asse Y. </td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Asse Y &gt; Oggetto modello dati</td>
   <td><p>Elemento di raccolta dei dati del modulo da tracciare sull'asse Y. Nel canale Stampa, l'oggetto del modello dati per l'asse Y deve essere di tipo Number.</p> <p>Scegliere due proprietà di tipo raccolta/array dello stesso oggetto del modello dati padre che abbiano un significato in relazione l'una all'altra per eseguire il grafico sull'asse X e Y di un grafico. </p> </td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Asse Y &gt; Funzione</td>
   <td>Funzione statistica/personalizzata da utilizzare per l'elaborazione dei valori sull'asse y.</td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Nascondi oggetto</td>
   <td>Selezionare questa opzione per nascondere il grafico nell'output finale.</td>
   <td>Stampa e Web</td>
  </tr>
  <tr>
   <td>Titolo</td>
   <td>Titolo del grafico. </td>
   <td>Stampa</td>
  </tr>
  <tr>
   <td>Altezza</td>
   <td>Altezza del grafico, in pixel.</td>
   <td>Stampa</td>
  </tr>
  <tr>
   <td>Larghezza</td>
   <td>Larghezza del grafico, in pixel. È possibile controllare la larghezza del grafico nel canale Web utilizzando il livello di stile o applicando un tema.</td>
   <td>Stampa</td>
  </tr>
  <tr>
   <td>Interruzione di pagina obbligatoria prima</td>
   <td>Selezionare questa opzione per aggiungere un'interruzione di pagina obbligatoria prima del grafico e posizionare il grafico sopra una nuova pagina. </td>
   <td>Stampa</td>
  </tr>
  <tr>
   <td>Interruzione di pagina obbligatoria dopo</td>
   <td>Selezionare questa opzione per aggiungere un'interruzione di pagina obbligatoria dopo il grafico e posizionare il contenuto che segue il grafico sopra una nuova pagina. </td>
   <td>Stampa</td>
  </tr>
  <tr>
   <td>Rientro</td>
   <td>Rientro del grafico a sinistra della pagina. </td>
   <td>Stampa</td>
  </tr>
  <tr>
   <td>Suggerimento</td>
   <td><p>Formato in cui la descrizione comando viene visualizzata al passaggio del mouse su un punto dati del grafico nel canale Web. Il valore predefinito è ${x}(${y}). A seconda del tipo di grafico, quando si posiziona il mouse su un punto, una barra o una sezione del grafico, le variabili ${x}e ${y} vengono sostituite dinamicamente con i valori corrispondenti sull'asse X e sull'asse Y e visualizzati nella descrizione comandi.</p> <p>Per disattivare la descrizione comandi, lasciare vuoto il campo <span class="uicontrol">Descrizione comandi</code>. Questa opzione non è applicabile ai grafici a linee e a superfici. Ad esempio, vedere <a href="#chartoutputprintweb">Esempio 1: Output grafico in stampa e Web</a>.</code></p> </td>
   <td>Web</td>
  </tr>
  <tr>
   <td>Configurazioni specifiche per i grafici</td>
   <td><p>Oltre alle configurazioni comuni, sono disponibili le seguenti configurazioni specifiche per i grafici:</p>
    <ul>
     <li><strong>Mostra legenda:  </strong>Mostra una legenda per il grafico a torta o a torta quando è attivato.</li>
     <li><strong>Posizione della legenda:  </strong>Specifica la posizione della legenda rispetto al grafico. Le opzioni disponibili sono Destra, Sinistra, In alto e In basso. Si consiglia di utilizzare la legenda sul lato destro del canale di stampa.</li>
     <li><strong>Raggio</strong> interno: Disponibile per i grafici ad anello per specificare il raggio (in pixel) del cerchio interno nel grafico.</li>
     <li><strong>Colore</strong> linea: Disponibile per i grafici Linea, Linea e Punto e Area, per specificare il colore della linea nel grafico.</li>
     <li><strong>Colore</strong> punto: Disponibile per i grafici Punto e Linea e Punto per specificare il colore dei punti nel grafico.<br /> </li>
     <li><strong>Colore</strong> area: Disponibile per i grafici ad area per specificare il colore dell'area sotto la linea del grafico.</li>
     <li><strong>Punto di riferimento &gt; Tipo di binding:  </strong>Disponibile per i grafici quadranti <strong> </strong>per specificare il tipo di binding per il punto di riferimento. Utilizzare la proprietà statica dell'oggetto testo o modello dati per definire il valore per il punto di riferimento.</li>
     <li><strong>Punto di riferimento &gt; asse X:  </strong>Disponibile per i grafici quadranti se si seleziona  <span class="uicontrol"></code> Static dall'elenco a discesa Binding Type (Tipo di binding) per specificare il valore dell'asse X per il punto di riferimento.</code></li>
     <li><strong>Punto di riferimento &gt; asse Y:  </strong>Disponibile per i grafici quadranti se si seleziona  <span class="uicontrol"></code> Static dall'elenco a discesa Binding Type (Tipo di binding) per specificare il valore dell'asse Y per il punto di riferimento.</code></li>
     <li><strong>Punto di riferimento &gt; Oggetto del modello dati per le serie:  </strong>Disponibile per più grafici Quadrante serie se si seleziona  <span class="uicontrol">Oggetto modello dati </code> dall'elenco a discesa Tipo di binding. Definisci le proprietà oggetto modello dati del modulo per identificare la serie per il punto di riferimento. </code></li>
     <li><strong>Punto di riferimento &gt; Valore oggetto modello dati per le serie:  </strong>Disponibile per più grafici Quadrante serie se si seleziona  <span class="uicontrol">Oggetto modello dati </code> dall'elenco a discesa Tipo di binding. Utilizzare la proprietà dell'oggetto modello dati modulo per le serie e il valore definito in questo campo per identificare le serie per il punto di riferimento.</code></li>
     <li><strong>Punto di riferimento &gt; Oggetto del modello dati per il punto di riferimento:  </strong>Disponibile per i grafici quadranti se si seleziona  <span class="uicontrol">Oggetto modello dati </code> dall'elenco a discesa Tipo di binding. Definire una proprietà dell'oggetto modello dati modulo di pari livello con le proprietà tracciate sull'asse X e sull'asse Y. Inoltre, per più serie, definire una proprietà dell'oggetto modello dati che sia un'entità figlia della proprietà dell'oggetto modello dati definita per la serie.</code></li>
     <li><strong>Punto di riferimento &gt; Valore oggetto modello dati per punto di riferimento:  </strong>Disponibile per i grafici quadranti se si seleziona  <span class="uicontrol">Oggetto modello dati </code> dall'elenco a discesa Tipo di binding. Utilizzare la proprietà dell'oggetto modello dati modulo per il punto di riferimento e il valore definito in questo campo per identificare il punto di riferimento per il grafico.<br /> <strong>Etichette quadranti &gt; In alto a sinistra: </strong> disponibili per i grafici quadranti per specificare il nome del quadrante in alto a sinistra.</code></li>
     <li><strong>Etichette quadranti &gt; In alto a destra:</strong> disponibili per i grafici quadranti per specificare il nome del quadrante in alto a destra.</li>
     <li><strong>Etichette quadranti &gt; In basso a destra:  </strong>Disponibile per i grafici Quadrante per specificare il nome del quadrante inferiore destro.</li>
     <li><strong>Etichette quadranti &gt; In basso a sinistra:  </strong>Disponibile per i grafici Quadrante per specificare il nome del quadrante in basso a sinistra.</li>
    </ul> </td>
   <td>Stampa e Web</td>
  </tr>
 </tbody>
</table>

## Utilizzare le funzioni nel grafico {#use-functions-in-chart}

È possibile configurare un grafico in modo da utilizzare le funzioni statistiche per calcolare i valori dai dati di origine per il grafico. Applicando le funzioni in un grafico, è possibile stampare dati non forniti direttamente dal modello dati del modulo.

![Funzioni nei grafici](assets/functions_charts_new.png)

Mentre il componente Grafico include alcune funzioni integrate, è possibile scrivere [funzioni personalizzate](#customfunctionsweb) e renderle disponibili per l&#39;utilizzo nella configurazione grafico del canale Web.

Per impostazione predefinita, con il componente Grafico sono disponibili le seguenti funzioni:

**Media (media)** Restituisce la media dei valori sull&#39;asse X o Y per un dato valore sull&#39;altro asse.

**** SumRestituisce la somma di tutti i valori sull&#39;asse X o Y per un valore specificato sull&#39;altro asse.

**** MaximumRestituisce il massimo dei valori sull&#39;asse X o Y per un valore specificato sull&#39;altro asse.

**** FrequenzaRestituisce il numero di valori sull&#39;asse X o Y per un valore specificato sull&#39;altro asse.

**** RangeRestituisce la differenza tra il massimo e il minimo dei valori sull&#39;asse X o Y per un valore specificato sull&#39;altro asse.

**Median** Restituisce il valore che separa i valori più alti e i valori più bassi a metà dell&#39;asse X o Y per un valore specificato sull&#39;altro asse.

**** MinimumRestituisce il minimo dei valori sull&#39;asse X o Y per un valore specificato sull&#39;altro asse.

**** ModeRestituisce il valore con la maggior parte delle occorrenze sull&#39;asse X o Y per un valore specificato sull&#39;altro asse.

Per ulteriori informazioni, vedere [Esempio 2: Applicazione delle funzioni Somma e Frequenza in un grafico a linee](#applicationsumfrequency).

### Funzioni personalizzate nel canale Web {#customfunctionsweb}

Oltre a utilizzare le funzioni predefinite nei grafici, è possibile scrivere funzioni personalizzate in JavaScript™ e renderle disponibili nell&#39;elenco delle funzioni del componente Grafico per il canale Web.

Una funzione utilizza una matrice o più valori e un nome di categoria come input e restituisce un valore. Esempio:

```javascript
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

Dopo aver scritto una funzione personalizzata, effettuate le seguenti operazioni per renderla disponibile per la configurazione del grafico:

1. Aggiungere la funzione personalizzata nella libreria client associata alla comunicazione interattiva pertinente. Per ulteriori informazioni, vedere [Configurazione dell&#39;azione di invio](/help/forms/using/configuring-submit-actions.md) e [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md).

1. Per visualizzare la funzione personalizzata nel menu a discesa Funzione, in CRXDe Lite, create un nodo `nt:unstructured` nella cartella delle app con le seguenti proprietà:

   * Aggiungete la proprietà `guideComponentType` con il valore `fd/af/reducer`. (mandatory)

   * Aggiungete la proprietà `value` a un nome completo della funzione JavaScript™ personalizzata. (obbligatorio) e impostarne il valore sul nome della funzione personalizzata, ad esempio Moltiplica.
   * Aggiungete la proprietà `jcr:description` con il valore da visualizzare come nome della funzione personalizzata che viene visualizzata nel menu a discesa Funzione. Ad esempio, **Moltiplica**.

   * Aggiungete la proprietà `qtip` con un valore che sarà una breve descrizione della funzione personalizzata. Viene visualizzata come una descrizione quando si passa il puntatore sul nome della funzione nell&#39;elenco a discesa **Function**.

1. Fare clic su **Salva tutto** per salvare la configurazione.

La funzione è ora disponibile per l&#39;utilizzo nel grafico.

## Esempio 1: Output grafico in stampa e Web {#chartoutputprintweb}

Nella scheda Base è possibile definire il tipo di grafico, le proprietà del modello dati del modulo di origine che contengono dati, le etichette da tracciare sull&#39;asse X e sull&#39;asse Y del grafico ed eventualmente la funzione statistica per calcolare i valori per il grafico.

Comprendiamo in dettaglio le informazioni minime richieste nelle proprietà di base, con l&#39;aiuto di un&#39;istruzione scheda generata utilizzando una comunicazione interattiva. Tenere presente che si desidera generare un grafico per rappresentare l&#39;importo di spese diverse nell&#39;istruzione. È possibile utilizzare diversi tipi di grafici per la stampa e l&#39;output Web della comunicazione interattiva.

### Grafico a colonne per Stampa {#columnchartprint}

A questo scopo, specificate le seguenti proprietà:

* **[!UICONTROL Nome]** : consente di specificare il nome del grafico.
* **[!UICONTROL Tipo]**  grafico - Selezionare  **** Colonna dall&#39;elenco a discesa.
* **[!UICONTROL Titolo]**  - Specifica il tipo di spesa per l&#39;asse X e l&#39;importo della transazione per l&#39;asse Y.
* **[!UICONTROL Oggetti]**  modello dati - Selezionare le proprietà dell&#39;oggetto modello dati per creare binding dei dati per l&#39;asse X (tipo di spesa) e l&#39;asse Y (importo transazione).

![Grafico a colonne nel canale di stampa di una comunicazione interattiva](assets/sample_chart_print_column_new.png)

Grafico a colonne nel canale di stampa di una comunicazione interattiva

### Grafico a torta per Web {#donutchartweb}

A questo scopo, specificate le seguenti proprietà:

* **[!UICONTROL Nome]** : consente di specificare il nome del grafico.
* **[!UICONTROL Tipo]**  grafico - Seleziona  **** Donutt dall&#39;elenco a discesa.
* **[!UICONTROL Oggetti]**  modello dati - Selezionare le proprietà dell&#39;oggetto modello dati per creare binding dei dati per l&#39;asse X (tipo di spesa) e l&#39;asse Y (importo transazione).
* **[!UICONTROL Raggio]**  interno - Specificate il valore Raggio interno come 150 per specificare il raggio (in pixel) del cerchio interno nel grafico.
* **[!UICONTROL Descrizione]** : utilizzate il formato predefinito ${x}(${y}) per visualizzare la descrizione comandi. La descrizione comandi viene visualizzata come segue: Tipo di spesa (importo transazione). Esempio: Debito per Bitcoin(10000).

![Grafico ad anello nel canale web di una comunicazione interattiva](assets/sample_chart_web_new.png)

Grafico ad anello nel canale web di una comunicazione interattiva

## Esempio 2: Applicazione delle funzioni Somma e Frequenza in un grafico a linee {#applicationsumfrequency}

Applicando le funzioni in un grafico, è possibile stampare dati non forniti direttamente dal modello dati del modulo. In questo esempio, utilizziamo un esempio di rendiconto sulla carta di credito per comprendere in che modo le funzioni Somma e Frequenza possono essere applicate al grafico.

![Grafico a linee senza funzione con due transazioni &quot;Debit for AirBnB&quot;](assets/line_chart_web_new.png)

Grafico a linee senza funzione con due transazioni &quot;Debit for AirBnB&quot;

### Sum function {#sum-function}

È possibile applicare la funzione sum per aggiungere valori di più istanze della stessa proprietà di dati e visualizzarla una sola volta. Ad esempio, nel grafico seguente, la funzione Somma è applicata sull&#39;asse Y per sommare l&#39;importo dei due Debiti per le transazioni AirBnB (2050 e 1050) e mostrare solo una transazione (3100).

La funzione Somma può rendere il grafico più utile quando si desidera raccogliere e visualizzare la somma per molte istanze della stessa proprietà data.

![Somma grafico a linee](assets/line_chart_web_sum_new.png)

### Funzione di frequenza {#frequency-function}

La funzione Frequenza restituisce il numero di valori dell&#39;asse Y per un dato valore sull&#39;altro asse. Con l&#39;applicazione della funzione Frequenza sull&#39;asse Y (Importo transazione), il grafico mostra che sono state rilevate due occorrenze di Debit per le transazioni AirBnB e una occorrenza degli altri tipi di transazioni.

![Frequenza grafico a linee](assets/line_chart_web_functions_frequency_new.png)

## Esempio 3: Grafico quadrante multiserie in Web {#example-multi-series-quadrant-chart-in-web}

Il grafico rappresenta l&#39;importo delle transazioni eseguite in un determinato intervallo di date. Il grafico Quadrante consente di dividere l&#39;area del grafico in quattro sezioni etichettate. Il carrello utilizza un punto di riferimento statico per gli assi X e Y. Utilizzate la funzione serie multipla per separare i dati in base al nome della banca.

A questo scopo, specificate le seguenti proprietà:

* **Nome:** specifica il nome del grafico.
* **Tipo di grafico:** selezionare  **** Quadrante dall&#39;elenco a discesa.

* Selezionare la casella di controllo **Serie multiple**.
* **Oggetto** modello dati: Specificare la proprietà dell&#39;oggetto modello dati per la serie. La proprietà dell&#39;oggetto modello dati per il nome della banca è un elemento padre delle proprietà dell&#39;oggetto modello dati tracciate sull&#39;asse X e sull&#39;asse Y.
* **Oggetti modello dati:** selezionare le proprietà dell&#39;oggetto modello dati per creare binding dei dati per l&#39;asse X (Data transazione) e l&#39;asse Y (Importo transazione).
* Nella sezione **Punto di riferimento**, selezionare **Static** come tipo di binding.

* Specificate i valori per i punti di riferimento dell’asse X e dell’asse Y.
* Specificate le etichette del quadrante per i quadranti In alto a sinistra, In alto a destra, In basso a destra e In basso a sinistra.
* Selezionare la casella di controllo **Mostra legende** per visualizzare i codici colore per i nomi bancari.

![Grafici quadranti](assets/charts_quadrant_example_new.png)

