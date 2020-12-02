---
title: Tabelle nei moduli adattivi
seo-title: Tabelle nei moduli adattivi
description: Il componente Tabella in  AEM Forms consente di creare tabelle in moduli adattivi reattivi ai layout mobili e di utilizzare anche componenti per tabelle XDP.
seo-description: Il componente Tabella in  AEM Forms consente di creare tabelle in moduli adattivi reattivi ai layout mobili e di utilizzare anche componenti per tabelle XDP.
uuid: 03436c81-42f0-430f-9e52-14a4ab0e877d
topic-tags: author
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc418da9-496f-4a2b-bfe4-2add3ac4f468
docset: aem65
translation-type: tm+mt
source-git-commit: 26a65772c43a5176d178bb6625604d18ac91e894
workflow-type: tm+mt
source-wordcount: '2302'
ht-degree: 0%

---


# Tabelle nei moduli adattivi{#tables-in-adaptive-forms}

L&#39;utilizzo delle tabelle rappresenta un modo efficace, semplificato e organizzato di presentare dati complessi. Consente agli utenti di identificare facilmente le informazioni e fornire gli input in una disposizione ordinata di righe e colonne. La maggior parte dei moduli provenienti da servizi finanziari e organizzazioni governative richiede tabelle di dati di grandi dimensioni per inserire numeri ed eseguire calcoli.

 AEM Forms fornisce un componente Tabella nel browser Componenti nella barra laterale che consente di creare tabelle in moduli adattivi. Alcune delle funzionalità chiave che fornisce sono:

* Layout reattivo su dispositivi mobili
* Righe e colonne configurabili
* Aggiunta ed eliminazione dinamica delle righe in fase di esecuzione
* Combinare o unire e dividere le celle
* Accessibile dagli assistenti vocali
* Layout personalizzato con CSS
* Compatibile e mappato con il componente tabella XDP
* Supporto per l&#39;aggiunta di righe o celle utilizzando elementi di tipo complesso XSD
* Unione di dati da un file XML

## Creare una tabella {#create-a-table}

Per creare una tabella, trascinate il componente Tabella dal browser Componenti nella barra laterale del modulo adattivo. Per impostazione predefinita, la tabella contiene due colonne e tre righe, inclusa la riga di intestazione.

![Componente tabella nella AEM barra laterale](assets/sidebar-tables.png)

### Informazioni sulle celle di intestazione e corpo {#about-header-and-body-cells}

Le celle di intestazione sono campi di testo. Per modificare l&#39;etichetta di un&#39;intestazione, fare clic con il pulsante destro del mouse sulla cella di intestazione e scegliere **Modifica**. Nella finestra di dialogo Modifica, aggiornare l&#39;etichetta nel campo **Valore** e fare clic su **OK**.

Per impostazione predefinita, le celle corpo sono caselle di testo. È possibile sostituire una cella corpo con qualsiasi altro componente di modulo adattivo disponibile nella barra laterale, ad esempio una casella numerica, un selettore data o un elenco a discesa.

Ad esempio, la prima riga corpo nella tabella seguente include come celle i componenti casella di testo, selezione data e elenco a discesa.

![celle di riga](assets/row-cell-types.png)

Per unire due o più celle corpo, selezionare le celle da unire, fare clic con il pulsante destro del mouse e selezionare **Merge**. È inoltre possibile dividere una cella unita facendo clic con il pulsante destro del mouse e selezionando **Dividi celle**.

### Aggiungere, eliminare, spostare righe e colonne {#add-delete-move-rows-and-columns}

È possibile aggiungere ed eliminare una riga o una colonna e spostare una riga verso l&#39;alto o il basso all&#39;interno di una tabella.

Per aggiungere o eliminare una riga o una colonna o spostare una riga, fare clic su una cella della riga o colonna. Nella parte superiore della colonna e a sinistra della riga viene visualizzato un menu a discesa. Il menu in alto contiene opzioni per aggiungere o eliminare la colonna, mentre il menu a sinistra consente di aggiungere, eliminare o spostare la riga.

* L&#39;operazione Aggiungi aggiunge una riga sotto o una colonna a destra della riga o colonna selezionata.
* L&#39;operazione Elimina elimina la riga o la colonna selezionata.
* L&#39;operazione Sposta su e Sposta giù sposta la riga selezionata verso l&#39;alto e verso il basso.

Il menu a discesa della riga fornisce inoltre l&#39;operazione Modifica per modificare le proprietà, le impostazioni e le opzioni di stile della riga.

![add-delete-move-row-column](assets/add-delete-move-row-column.png)

>[!NOTE]
>
>Anche se è possibile aggiungere un numero qualsiasi di righe in una tabella, il numero massimo di colonne è sei. Inoltre, non è possibile eliminare la riga di intestazione dalla tabella.

### Aggiungi descrizione tabella {#add-table-description}

È possibile aggiungere una descrizione della tabella per spiegare in che modo le informazioni sono organizzate che gli assistenti vocali possono interpretare e leggere. Per aggiungere la descrizione:

1. Selezionare la tabella e toccare ![cmppr](assets/cmppr.png) per visualizzarne le proprietà nella barra laterale.
1. Specificare un riepilogo nella scheda Accessibilità.
1. Fare clic su **Fine**.

### Ordinare le colonne in una tabella {#sortcolumnstable}

È possibile ordinare i dati in base a qualsiasi colonna di una tabella nel modulo adattivo. I valori nella colonna possono essere ordinati in ordine crescente o decrescente.

L&#39;ordinamento può essere applicato alle colonne di tabella contenenti:

* Testo statico
* Proprietà dell&#39;oggetto modello dati
* Combinazione di proprietà statiche dell&#39;oggetto testo e modello dati

Per applicare l&#39;ordinamento alle colonne di tabella, le celle delle colonne di tabella devono contenere i seguenti componenti: Casella numerica, Timbro numerico, Campo immissione data, Selettore data, Testo o Casella di testo.

Per abilitare l&#39;ordinamento:

1. Selezionare la tabella e toccare ![configure_icon](assets/configure_icon.png) (Configura). È inoltre possibile selezionare la tabella utilizzando il browser **Content** nella barra laterale della comunicazione interattiva.
1. Selezionare **Abilita ordinamento**.
1. Toccate ![done_icon](assets/done_icon.png) per salvare le proprietà della tabella. Le icone di ordinamento, le frecce su e giù, nelle intestazioni delle colonne, indicano che l&#39;ordinamento è stato attivato.

   ![Abilita ordinamento](assets/enable_sorting_new.png)

1. Passate alla modalità **Anteprima** per visualizzare l&#39;output. La tabella viene ordinata automaticamente in base alla prima colonna della tabella.
1. Fate clic sull’intestazione della colonna per ordinare i valori in base alla colonna.

   Un&#39;intestazione di colonna con una freccia su indica che la tabella è ordinata in base a tale colonna. Inoltre, i valori della colonna vengono visualizzati in ordine crescente.

   ![Ordinamento in ordine crescente](assets/sorting_ascending_new.png)

   Analogamente, un&#39;intestazione di colonna con una freccia rivolta verso il basso rappresenta la visualizzazione dei valori della colonna in ordine decrescente.

   È inoltre possibile apportare modifiche alla tabella in modalità **Anteprima** e fare di nuovo clic sull&#39;intestazione della colonna per ordinare i valori della colonna.

## Configurare lo stile di tabella {#configure}

È possibile definire lo stile di una tabella utilizzando la modalità Stile nella barra degli strumenti della pagina. Per passare alla modalità di stile e modificare lo stile della tabella, procedere come segue.

1. Nella barra degli strumenti della pagina, prima di Preview, toccare ![canvas-drop-down](assets/canvas-drop-down.png) > **Style**.

1. Nella barra laterale selezionate la tabella e toccate il pulsante di modifica ![pulsante di modifica](assets/edit-button.png).
Potete visualizzare le proprietà di stile nella barra laterale.

![Proprietà di stile di una tabella](assets/style-table.png)

>[!NOTE]
>
>È possibile modificare il tema colore per le righe di intestazione e le righe corpo modificando i valori delle variabili LESS. Per ulteriori informazioni, vedere [Temi in  AEM Forms](/help/forms/using/themes.md) [](/help/forms/using/creating-custom-adaptive-form-themes.md).

## Aggiunta o eliminazione dinamica di una riga {#add-or-delete-a-row-dynamically}

Le tabelle forniscono supporto out-of-the-box per l&#39;aggiunta o l&#39;eliminazione dinamica di righe in fase di esecuzione.

1. Selezionare una riga di tabella e toccare ![cmppr](assets/cmppr.png).
1. Nella scheda Impostazioni ripetizione, specificare i conteggi minimo e massimo per limitare il numero di righe nella tabella.
1. Fare clic su **Fine**.

In fase di esecuzione, saranno visualizzati i pulsanti **+** e *-* per aggiungere o eliminare una riga.

![add-delete-rows-dynamic](assets/add-delete-rows-dynamically.png)

>[!NOTE]
>
>L&#39;aggiunta o l&#39;eliminazione dinamica di una riga non è supportata nelle intestazioni nel layout mobile sinistro delle tabelle.

## Espressioni in una tabella {#expressions-in-a-table}

Le tabelle nei moduli adattivi consentono di scrivere espressioni in JavaScript per indurre comportamenti quali mostrare o nascondere una tabella o una riga, sommare tutti i numeri e mostrare il totale in una cella, attivare o disattivare una cella, convalidare l&#39;input dell&#39;utente e così via. Queste espressioni utilizzano le API del modello di script dei moduli adattivi.

Mentre tabelle e righe supportano solo le espressioni di visibilità per controllarne la visibilità in base al valore restituito da un&#39;espressione, le celle supportano le seguenti espressioni:

* **Script di inizializzazione:** per eseguire un&#39;azione all&#39;inizializzazione di un campo.
* **script Conferma valore:** per modificare i componenti di un modulo dopo la modifica del valore di un campo.

>[!NOTE]
>
>Se lo script XFA change/exit è applicato anche allo stesso campo, lo script XFA change/exit viene eseguito prima dello script Value Commit.

* **Calcola espressioni**: per calcolare automaticamente il valore di un campo.
* **Espressioni** di convalida: per convalidare un campo.
* **Espressioni** di accesso: per attivare/disattivare un campo.
* **Espressione** di visibilità: per controllare la visibilità di un campo e di un pannello.

L’espressione di visibilità per una tabella o una riga può essere definita nella scheda Proprietà pannello della finestra di dialogo corrispondente del componente Modifica. Le espressioni per una cella possono essere definite nella scheda Script della finestra di dialogo del componente Modifica.

Per l&#39;elenco completo delle classi, degli eventi, degli oggetti e delle API pubbliche dei moduli adattivi, vedere [Riferimento API della libreria JavaScript per i moduli adattivi](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## Layout per dispositivi mobili {#mobile-layouts}

Le tabelle nei moduli adattivi offrono un&#39;esperienza senza confronti per i dispositivi mobili grazie ai layout fluidi e reattivi.  AEM Forms offre due tipi di layout mobili per le tabelle: Intestazioni sulle colonne sinistra e Comprimibili.

È possibile configurare un layout mobile per una tabella dalla scheda Stile della finestra di dialogo del componente Modifica per una tabella.

### Intestazioni a sinistra {#headers-on-left}

Nel layout Intestazioni a sinistra, l’intestazione della tabella viene trasposta a sinistra, con una sola cella che appare su un’intestazione. Ogni riga in questo layout viene visualizzata come una sezione distinta. Le immagini seguenti confrontano una tabella su un desktop con quella su un dispositivo mobile.

![visualizzazione desktop](assets/desktopview_new.png)

Vista desktop di una tabella con il layout Intestazione a sinistra

![Intestazioni a sinistra](assets/headersontheleft_new.png)

Vista mobile di una tabella con il layout Intestazione a sinistra

### Layout colonne comprimibili {#collapsible-columns-layout}

Nel layout della colonna Comprimibile, le colonne della tabella vengono ridotte per mostrare una o due colonne, a seconda della dimensione del dispositivo, mentre le altre colonne vengono ridotte. È possibile fare clic sull&#39;icona di compressione/espansione per visualizzare altre colonne nella tabella.

>[!NOTE]
>
>Anche se il layout di colonna Comprimibile è ottimizzato per i dispositivi mobili, funzionerà anche su desktop, se la larghezza disponibile non è sufficiente per mostrare tutte le colonne di una tabella.

Le immagini seguenti confrontano l&#39;aspetto di una tabella su un dispositivo con colonne compresse ed espanse.

![compresso-column](assets/collapsed-column.png)

Colonne compresse di una tabella con solo due colonne visualizzate su un dispositivo mobile

![compresso_column](assets/collapsible_column.png)

Colonna estesa di una tabella su un dispositivo mobile

## Unisci dati in una tabella {#merge-data-in-a-table}

Le tabelle in moduli adattivi consentono di compilare la tabella in fase di esecuzione utilizzando i dati provenienti da un file XML. Il file XML di dati può risiedere nel file system locale del computer in cui è in esecuzione  server AEM Forms o nell&#39;archivio CRX.

Esempio della tabella di riepilogo delle transazioni bancarie seguente che si desidera compilare con i dati provenienti da un file XML.

![data-merge-table](assets/data-merge-table.png)

In questo esempio, la proprietà Nome elemento per:

* la riga è **Riga1**
* la cella corpo in Data transazione è **tableItem1**
* la cella corpo in Descrizione è **tableItem2**
* la cella corpo sotto il tipo di transazione è **type**
* la cella corpo sotto Importo in USD è **tableItem3**

Il file XML che contiene i dati nel formato seguente:

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
 <typeSelect>0</typeSelect>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Purchase laptop</tableItem2>
      <type>0</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Transport expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-01-08</tableItem1>
      <tableItem2>Laser printer</tableItem2>
      <type>0</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2014-12-08</tableItem1>
      <tableItem2>Credit card payment</tableItem2>
      <type>0</type>
      <tableItem3>300</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-06</tableItem1>
      <tableItem2>Interest earnings</tableItem2>
      <type>1</type>
      <tableItem3>12000</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-05</tableItem1>
      <tableItem2>Payment from a client</tableItem2>
      <type>1</type>
      <tableItem3>500</tableItem3>
 </Row1>
 <Row1>
      <tableItem1>2015-01-08</tableItem1>
      <tableItem2>Food expense</tableItem2>
      <type>0</type>
      <tableItem3>120</tableItem3>
 </Row1>
 </data>
  </afUnboundData>
  <afBoundData>
    <data/>
  </afBoundData>
  <afBoundData/>
</afData>
```

Nell&#39;XML di esempio, i dati per una riga sono definiti dai tag `<Row1>`, che è il nome dell&#39;elemento per la riga nella tabella. All&#39;interno del tag `<Row1>`, i dati di ciascuna cella sono definiti all&#39;interno del tag relativo al nome dell&#39;elemento, ad esempio `<tableItem1>`, `<tableItem2>`, `<tableItem3>` e `<type>`.

Per unire questi dati alla tabella in fase di esecuzione, è necessario indirizzare il modulo adattivo contenente la tabella nella posizione XML assoluta con wcmmode disattivato. Ad esempio, se il modulo adattivo si trova in corrispondenza di *https://localhost:4502/myForms/bankTransaction.html* e il file XML di dati viene salvato in corrispondenza di *C:/myTransactions/bankSummary.xml*, è possibile visualizzare la tabella con i dati al seguente URL:

*https://localhost:4502/myForms/bankTransaction.html?dataRef=file:/// C:/myTransactions/bankSummary.xml&amp;wcmmode=disabled*

![tabella unita ai dati](assets/data-merged-table.png)

## Utilizzare componenti XDP e tipi complessi XSD {#use-xdp-components-and-xsd-complex-types}

Se è stato creato un modulo adattivo basato su un modello di modulo XFA, gli elementi XFA sono disponibili nella scheda Modello dati di AEM Content Finder. È possibile trascinare questi elementi XFA, incluse le tabelle, nel modulo adattivo.

L’elemento tabella XFA è mappato sul componente Tabella e funziona out-of-the-box nei moduli adattivi. Tutte le proprietà e le funzionalità della tabella XDP vengono mantenute quando vengono spostate in un modulo adattivo e potete eseguire qualsiasi operazione su di esso, come avviene per la tabella di moduli adattivi nativi. Ad esempio, se una riga in una tabella XDP è contrassegnata come ripetibile, viene ripetuta anche se rilasciata in moduli adattivi.

È inoltre possibile trascinare il sottomodulo XDP per aggiungere una nuova riga nella tabella. Tuttavia, tenere presente che il rilascio di un sottomodulo nidificato non funziona.

>[!NOTE]
>
>Una tabella XDP senza riga di intestazione non verrà mappata al componente Tabella modulo adattivo. Verrà invece mappato sul componente Pannello modulo adattivo con layout fluido. Inoltre, quando si aggiunge una tabella nidificata da un XDP a un modulo adattivo, la tabella esterna viene convertita in un pannello mantenendo la tabella interna.

È inoltre possibile trascinare un gruppo di elementi di tipo complesso XSD per creare una riga di tabella. Viene creata una nuova riga immediatamente sotto la riga in cui sono stati eliminati gli elementi. Le celle create utilizzando gli elementi di tipo complesso XSD mantengono un riferimento di binding all&#39;XSD. È inoltre possibile sostituire una cella corpo con un elemento di tipo complesso XSD rilasciando l&#39;elemento sulla cella.

>[!NOTE]
>
>Il numero di elementi in un componente tabella XDP, un sottomodulo o un tipo complesso XSD non può superare il numero di celle in una riga. Ad esempio, non è possibile rilasciare quattro elementi su una riga con solo tre celle. Ne risulterà un errore.
>
>Se il numero di elementi è inferiore al numero di celle in una riga, la nuova riga aggiunge prima le celle in base agli elementi, quindi le celle predefinite vengono aggiunte per riempire le celle rimanenti nella riga. Ad esempio, se rilasci un gruppo di tre elementi in una riga con quattro celle, le prime tre celle si basano sugli elementi rilasciati e la cella rimanente sarà quella predefinita.

## Considerazioni chiave {#key-considerations}

* Se si spostano le righe verso l&#39;alto o il basso durante la creazione di una tabella basata su XSD, alcuni dati persi dalle righe della tabella vengono visualizzati nell&#39;XML di dati generato all&#39;invio del modulo.
* A ogni cella corpo di una tabella predefinita è associato un nome di elemento predefinito. Se si aggiunge un&#39;altra tabella nel modulo adattivo, le celle corpo predefinite della nuova tabella avranno lo stesso nome di elemento della prima tabella. In questo caso, i dati generati al momento dell&#39;invio del modulo includeranno i dati nelle celle corpo predefinite di una sola tabella. Pertanto, è necessario rinominare i nomi degli elementi per le celle corpo predefinite in modo da mantenerle univoche tra le tabelle ed evitare la perdita di dati.

   Questo è applicabile solo alle celle corpo predefinite. Se si aggiungono più righe o colonne a una tabella, verranno generati automaticamente nomi di elementi univoci per le celle corpo non predefinite.

