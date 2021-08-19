---
title: Tabelle nei moduli adattivi
seo-title: Tabelle nei moduli adattivi
description: Il componente Tabella di AEM Forms consente di creare tabelle in moduli adattivi reattivi ai layout per dispositivi mobili e di utilizzare componenti per tabelle XDP.
seo-description: Il componente Tabella di AEM Forms consente di creare tabelle in moduli adattivi reattivi ai layout per dispositivi mobili e di utilizzare componenti per tabelle XDP.
uuid: 03436c81-42f0-430f-9e52-14a4ab0e877d
topic-tags: author
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc418da9-496f-4a2b-bfe4-2add3ac4f468
docset: aem65
feature: Moduli adattivi
exl-id: 1a139530-27bd-44da-8bf4-5b375e75cf32
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '2430'
ht-degree: 0%

---

# Tabelle nei moduli adattivi{#tables-in-adaptive-forms}

L’utilizzo delle tabelle rappresenta un modo efficace, semplificato e organizzato di presentare dati complessi. Consente agli utenti di identificare facilmente le informazioni e fornire gli input in una disposizione ordinata di righe e colonne. La maggior parte dei moduli dei servizi finanziari e delle organizzazioni governative richiede tabelle di dati di grandi dimensioni per inserire numeri ed eseguire calcoli.

AEM Forms fornisce un componente Tabella nel browser Componenti nella barra laterale che consente di creare tabelle nei moduli adattivi. Alcune delle funzionalità chiave che offre sono:

* Layout reattivo su dispositivi mobili
* Righe e colonne configurabili
* Aggiunta e eliminazione dinamiche delle righe in fase di runtime
* Combinare o unire celle e dividerle
* Accessibile dagli assistenti vocali
* Layout personalizzato con CSS
* Compatibile e mappato con il componente tabella XDP
* Supporto per l&#39;aggiunta di righe o celle utilizzando elementi di tipo complesso XSD
* Unione di dati da un file XML

## Creare una tabella {#create-a-table}

Per creare una tabella, trascinate il componente Tabella dal browser Componenti nella barra laterale del modulo adattivo. Per impostazione predefinita, la tabella contiene due colonne e tre righe, inclusa la riga di intestazione.

![Componente tabella nella barra laterale AEM](assets/sidebar-tables.png)

### Informazioni sulle celle di intestazione e corpo {#about-header-and-body-cells}

Le celle di intestazione sono campi di testo. Per modificare l&#39;etichetta di un&#39;intestazione, fare clic con il pulsante destro del mouse sulla cella di intestazione e fare clic su **Modifica**. Nella finestra di dialogo Modifica, aggiorna l’etichetta nel campo **Valore** e fai clic su **OK**.

Per impostazione predefinita, le celle corpo sono caselle di testo. È possibile sostituire una cella corpo con qualsiasi altro componente di moduli adattivi disponibile nella barra laterale, ad esempio una casella numerica, un selettore data o un elenco a discesa.

Ad esempio, la prima riga corpo della tabella seguente include come celle i componenti casella di testo, selezione data e elenco a discesa.

![tipi di celle a riga](assets/row-cell-types.png)

Per unire due o più celle corpo, selezionare le celle da unire, fare clic con il pulsante destro del mouse e selezionare **Unisci**. Inoltre, è possibile dividere una cella unita facendo clic con il pulsante destro del mouse e selezionando **Dividi celle**.

### Aggiungi, elimina, sposta righe e colonne {#add-delete-move-rows-and-columns}

È possibile aggiungere ed eliminare una riga o una colonna e spostare una riga verso l’alto o il basso all’interno di una tabella.

Per aggiungere o eliminare una riga o una colonna o spostare una riga, fare clic su una cella della riga o della colonna. Nella parte superiore della colonna e a sinistra della riga viene visualizzato un menu a discesa. Il menu in alto fornisce le opzioni per aggiungere o eliminare la colonna, mentre il menu a sinistra consente di aggiungere, eliminare o spostare la riga.

* L’operazione Aggiungi aggiunge una riga sotto o una colonna a destra della riga o colonna selezionata.
* L’operazione Elimina elimina la riga o la colonna selezionata.
* L’operazione Sposta su e Sposta giù sposta la riga selezionata verso l’alto o verso il basso.

Il menu a discesa della riga fornisce inoltre l’operazione Modifica per modificare le proprietà, le impostazioni e le opzioni di stile della riga.

![add-delete-move-row-column](assets/add-delete-move-row-column.png)

>[!NOTE]
>
>È possibile aggiungere un qualsiasi numero di righe in una tabella, ma il numero massimo di colonne è sei. Inoltre, non è possibile eliminare la riga di intestazione dalla tabella.

### Aggiungi descrizione tabella {#add-table-description}

È possibile aggiungere una descrizione della tabella per spiegare come sono organizzate le informazioni che gli assistenti vocali possono interpretare e leggere. Per aggiungere la descrizione:

1. Seleziona la tabella e tocca ![cmppr](assets/cmppr.png) per visualizzarne le proprietà nella barra laterale.
1. Specificare il riepilogo nella scheda Accessibilità.
1. Fare clic su **Fine**.

### Ordinare le colonne in una tabella {#sortcolumnstable}

Puoi ordinare i dati in base a qualsiasi colonna di una tabella nel modulo adattivo. I valori della colonna possono essere ordinati in ordine crescente o decrescente.

L’ordinamento può essere applicato alle colonne della tabella contenenti:

* Testo statico
* Proprietà dell&#39;oggetto modello dati
* Combinazione delle proprietà dell’oggetto modello dati e testo statico

Per applicare l’ordinamento alle colonne di una tabella, le celle di colonna della tabella devono contenere uno dei seguenti componenti: Casella numerica, Passaggio numerico, Campo di immissione data, Selettore data, Testo o Casella di testo.

Per abilitare l’ordinamento:

1. Seleziona la tabella e tocca ![configure_icon](assets/configure_icon.png) (Configura). Puoi anche selezionare la tabella utilizzando il browser **Contenuto** nella barra laterale della comunicazione interattiva.
1. Selezionare **Abilita ordinamento**.
1. Tocca ![done_icon](assets/done_icon.png) per salvare le proprietà della tabella. Le icone di ordinamento, le frecce su e giù nelle intestazioni delle colonne indicano che l’ordinamento è stato attivato.

   ![Abilita ordinamento](assets/enable_sorting_new.png)

1. Passa alla modalità **Anteprima** per visualizzare l&#39;output. La tabella viene ordinata automaticamente in base alla prima colonna della tabella.
1. Fai clic sull’intestazione della colonna per ordinare i valori in base alla colonna.

   Un’intestazione di colonna con una freccia su indica che la tabella è ordinata in base a tale colonna. Inoltre, i valori nella colonna vengono visualizzati in ordine crescente.

   ![Ordinamento crescente](assets/sorting_ascending_new.png)

   Analogamente, un’intestazione di colonna con una freccia giù rappresenta la visualizzazione dei valori della colonna in ordine decrescente.

   È inoltre possibile apportare modifiche alla tabella in modalità **Anteprima** e fare di nuovo clic sull&#39;intestazione della colonna per ordinare i valori della colonna.

## Impostare la larghezza della colonna per una tabella {#set-column-width}

Esegui i seguenti passaggi per impostare la larghezza della colonna per una tabella:

1. Nella scheda **[!UICONTROL Contenuto]** , tocca il componente **[!UICONTROL Tabella]** e tocca l’icona Configura (![Configura](assets/configure-icon.svg)).

1. Immettere l&#39;elenco di valori separati da virgole nel campo **[!UICONTROL Larghezza colonna]** per specificare la larghezza proporzionale di ciascuna colonna della tabella. Ad esempio, per una tabella che include 3 colonne, specificando 2,4,6 come valore nel campo **[!UICONTROL Larghezza colonna]**, si imposta la larghezza delle colonne su 2/12 per la prima colonna, 4/12 per la seconda colonna e 6/12 per la terza colonna. 2/12 in quanto la larghezza della prima colonna si riferisce a un sesto della larghezza della tabella. Analogamente, 4/12 imposta la seconda larghezza della colonna come un terzo della larghezza della tabella e 6/12 imposta la terza larghezza della colonna come metà della larghezza della tabella.

## Configurare lo stile di tabella {#configure}

È possibile definire lo stile di una tabella utilizzando la modalità Stile nella barra degli strumenti della pagina. Esegui i seguenti passaggi per passare alla modalità stile e modificare lo stile della tabella

1. Nella barra degli strumenti della pagina, prima di Anteprima, tocca ![a discesa canvas](assets/canvas-drop-down.png) > **Stile**.

1. Nella barra laterale seleziona la tabella e tocca il pulsante di modifica ![edit-button](assets/edit-button.png).
Le proprietà di stile vengono visualizzate nella barra laterale.

![Proprietà di stile di una tabella](assets/style-table.png)

>[!NOTE]
>
>È possibile modificare il tema colore per le righe di intestazione e corpo modificando i valori delle variabili LESS. Per ulteriori informazioni, consulta [Temi in AEM Forms](/help/forms/using/themes.md).

## Aggiungere o eliminare una riga in modo dinamico {#add-or-delete-a-row-dynamically}

Le tabelle forniscono supporto predefinito per l’aggiunta o l’eliminazione dinamica di righe in fase di runtime.

1. Seleziona una riga di tabella e tocca ![cmppr](assets/cmppr.png).
1. Nella scheda Ripeti impostazioni specificare i conteggi minimo e massimo per limitare il numero di righe nella tabella.
1. Fare clic su **Fine**.

In fase di esecuzione, i pulsanti **+** e *-* vengono visualizzati per aggiungere o eliminare una riga.

![add-delete-rows-dinamicamente](assets/add-delete-rows-dynamically.png)

>[!NOTE]
>
>L’aggiunta o l’eliminazione dinamica di una riga non è supportata nelle intestazioni nel layout mobile sinistro delle tabelle.

## Espressioni in una tabella {#expressions-in-a-table}

Le tabelle nei moduli adattivi consentono di scrivere espressioni in JavaScript per indurre comportamenti come mostrare o nascondere una tabella o una riga, sommare tutti i numeri e mostrare il totale in una cella, abilitare o disabilitare una cella, convalidare l’input dell’utente e così via. Queste espressioni utilizzano API per modelli di script di moduli adattivi.

Mentre tabelle e righe supportano solo espressioni di visibilità per controllarne la visibilità in base al valore restituito da un&#39;espressione, le celle supportano le seguenti espressioni:

* **Script di inizializzazione:** per eseguire un&#39;azione sull&#39;inizializzazione di un campo.
* **Script di commit dei valori:** per modificare i componenti di un modulo dopo la modifica del valore di un campo.

>[!NOTE]
>
>Se lo script XFA change/exit viene applicato anche allo stesso campo, lo script XFA change/exit viene eseguito prima dello script Value Commit.

* **Calcola espressioni**: per calcolare automaticamente il valore di un campo.
* **Espressioni** di convalida: per convalidare un campo.
* **Espressioni** di accesso: per abilitare/disabilitare un campo.
* **Espressione** di visibilità: per controllare la visibilità di un campo e di un pannello.

L’espressione di visibilità per una tabella o una riga può essere definita nella scheda Proprietà pannello della finestra di dialogo corrispondente del componente Modifica . Le espressioni per una cella possono essere definite nella scheda Script della finestra di dialogo del componente Modifica.

Per l&#39;elenco completo delle classi, degli eventi, degli oggetti e delle API pubbliche dei moduli adattivi, consulta [Riferimento API della libreria JavaScript per i moduli adattivi](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## Layout dei dispositivi mobili {#mobile-layouts}

Le tabelle nei moduli adattivi offrono ai dispositivi mobili un’esperienza senza pari a causa dei layout fluidi e reattivi. AEM Forms offre due tipi di layout per dispositivi mobili per le tabelle: intestazioni a sinistra e colonne comprimibili.

Puoi configurare un layout mobile per una tabella dalla scheda Stile della finestra di dialogo Modifica componente per una tabella.

### Intestazioni a sinistra {#headers-on-left}

Nel layout Intestazioni a sinistra, l’intestazione della tabella viene trasposta a sinistra con una sola cella che appare su un’intestazione. Ogni riga in questo layout viene visualizzata come una sezione distinta. Le immagini seguenti confrontano una tabella su un desktop con quella su un dispositivo mobile.

![vista desktop](assets/desktopview_new.png)

Vista desktop di una tabella con layout Intestazione a sinistra

![Intestazioni a sinistra](assets/headersontheleft_new.png)

Visualizzazione mobile di una tabella con layout Intestazione a sinistra

### Layout delle colonne comprimibili {#collapsible-columns-layout}

Nel layout a colonne comprimibili, le colonne della tabella vengono compresse per mostrare una o due colonne, a seconda delle dimensioni del dispositivo, mentre le altre colonne vengono compresse. È possibile fare clic sull’icona di compressione/espansione per visualizzare altre colonne della tabella.

>[!NOTE]
>
>Anche se il layout di colonna Comprimibile è ottimizzato per i dispositivi mobili, funziona anche sul desktop, se la larghezza disponibile non è sufficiente per mostrare tutte le colonne di una tabella.

Le immagini seguenti confrontano l’aspetto di una tabella su un dispositivo con colonne compresse ed espanse.

![colonna compressa](assets/collapsed-column.png)

Colonne compresse di una tabella con solo due colonne visualizzate su un dispositivo mobile

![comprimibile_colonna](assets/collapsible_column.png)

Colonna espansa di una tabella su un dispositivo mobile

## Unione di dati in una tabella {#merge-data-in-a-table}

Le tabelle nei moduli adattivi consentono di compilare la tabella in fase di esecuzione utilizzando i dati di un file XML. Il file XML di dati può trovarsi nel file system locale del computer in cui è in esecuzione il server AEM Forms o nell&#39;archivio CRX.

Esempio della seguente tabella di riepilogo delle transazioni bancarie che si desidera compilare con i dati di un file XML.

![data-merge-table](assets/data-merge-table.png)

In questo esempio, la proprietà Nome elemento per:

* la riga è **Riga1**
* la cella corpo in Data transazione è **tableItem1**
* la cella corpo sotto Descrizione è **tableItem2**
* la cella corpo sotto il tipo di transazione è **type**
* la cella corpo sotto Importo in USD è **tableItem3**

File XML contenente i dati nel formato seguente:

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

Nell’XML di esempio, i dati di una riga sono definiti dai tag `<Row1>` , che è il nome dell’elemento per la riga nella tabella. All’interno del tag `<Row1>` , i dati di ogni cella vengono definiti all’interno del tag relativo al nome dell’elemento, ad esempio `<tableItem1>`, `<tableItem2>`, `<tableItem3>` e `<type>`.

Per unire questi dati alla tabella in fase di runtime, è necessario indirizzare il modulo adattivo contenente la tabella al percorso XML assoluto con wcmmode disattivato. Ad esempio, se il modulo adattivo si trova in *https://localhost:4502/myForms/bankTransaction.html* e il file XML di dati viene salvato in *C:/myTransactions/bankSummary.xml*, è possibile visualizzare la tabella con i dati al seguente URL:

*https://localhost:4502/myForms/bankTransaction.html?dataRef=file:/// C:/myTransactions/bankSummary.xml&amp;wcmmode=disabled*

![data-merge-table](assets/data-merged-table.png)

## Utilizzare componenti XDP e tipi complessi XSD {#use-xdp-components-and-xsd-complex-types}

Se hai creato un modulo adattivo basato su un modello di modulo XFA, gli elementi XFA sono disponibili nella scheda Modello dati di AEM Content Finder. Puoi trascinare questi elementi XFA, incluse le tabelle, nel modulo adattivo.

L’elemento di tabella XFA è mappato sul componente Tabella e funziona preconfigurato nei moduli adattivi. Tutte le proprietà e le funzionalità della tabella XDP vengono mantenute quando vengono spostate in forma adattiva e puoi eseguire qualsiasi operazione su di essa, proprio come per la tabella di moduli adattivi nativi. Ad esempio, se una riga in una tabella XDP è contrassegnata come ripetibile, viene ripetuta anche quando viene rilasciata in moduli adattivi.

È inoltre possibile trascinare il sottomodulo XDP per aggiungere una nuova riga nella tabella. Tuttavia, il rilascio di un sottomodulo nidificato non funziona.

>[!NOTE]
>
>Una tabella XDP senza riga di intestazione non verrà mappata al componente Tabella modulo adattivo. Al contrario, verrà mappato sul componente per pannello adattivo con layout fluido. Inoltre, quando si aggiunge una tabella nidificata da un XDP a un modulo adattivo, la tabella esterna viene convertita in un pannello mantenendo la tabella interna.

Inoltre, puoi trascinare un gruppo di elementi di tipo complesso XSD per creare una riga di tabella. Viene creata una nuova riga immediatamente sotto la riga in cui sono stati rilasciati gli elementi. Le celle create utilizzando gli elementi di tipo complesso XSD mantengono un riferimento di binding a XSD. È inoltre possibile sostituire una cella corpo con un elemento di tipo complesso XSD rilasciando l&#39;elemento sulla cella.

>[!NOTE]
>
>Il numero di elementi in un componente tabella XDP, un sottomodulo o un tipo complesso XSD non può superare il numero di celle in una riga. Ad esempio, non è possibile rilasciare quattro elementi su una riga con solo tre celle. Si tradurrà in un errore.
>
>Se il numero di elementi è inferiore al numero di celle di una riga, la nuova riga aggiunge prima le celle in base agli elementi, quindi le celle predefinite vengono aggiunte per riempire le celle rimanenti della riga. Ad esempio, se rilasci un gruppo di tre elementi in una riga con quattro celle, le prime tre celle si basano sugli elementi saltati e la cella rimanente sarà la cella predefinita della tabella.

## Considerazioni fondamentali {#key-considerations}

* Se si spostano le righe in alto e in basso durante l’authoring di una tabella basata su XSD, alcuni dati persi dalle righe di tabella vengono visualizzati nell’XML dati generato all’invio del modulo.
* A ogni cella corpo di una tabella predefinita è associato un nome di elemento predefinito. Se si aggiunge un’altra tabella nel modulo adattivo, le celle del corpo predefinite nella nuova tabella avranno lo stesso nome di elemento della prima tabella. In questo caso, i dati generati al momento dell’invio del modulo includeranno i dati nelle celle corpo predefinite di una sola tabella. Assicurati pertanto di rinominare i nomi degli elementi per le celle corpo predefinite in modo da mantenerle univoche tra le tabelle ed evitare la perdita di dati.

   Si noti che questo è applicabile solo alle celle corpo predefinite. Se si aggiungono più righe o colonne a una tabella, verranno generati automaticamente nomi di elementi univoci per le celle corpo non predefinite.
