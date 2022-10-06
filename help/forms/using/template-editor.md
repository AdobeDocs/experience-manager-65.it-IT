---
title: Modelli di modulo adattivi
seo-title: Adaptive Form Templates
description: Creare modelli di modulo adattivo definendo la struttura di base e il contenuto iniziale del modulo utilizzando l’Editor modelli.
seo-description: Create adaptive form templates by defining the basic structure and initial form content using the Template Editor.
uuid: 317ca3ab-f809-49a7-a063-9d0c17a35fe4
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b21a48ba-eccd-4bb5-9b92-3039026ddf2a
docset: aem65
feature: Adaptive Forms
exl-id: d7287ee7-fb4e-4d47-b37e-0a9260344070
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 0%

---

# Modelli di modulo adattivi{#adaptive-form-templates}

Quando si crea un modulo, è possibile aggiungere campi e componenti per definire la struttura del modulo, il contenuto e le azioni nell’editor. Aggiungi campi e componenti nel `guideRootPanel` del contenitore modulo. Con l’Editor modelli è possibile creare un modello che contiene la struttura di base e il contenuto iniziale utilizzabili dagli autori per creare moduli.

Ad esempio, si desidera che tutti gli autori dei moduli dispongano di determinate caselle di testo, pulsanti di navigazione e un pulsante di invio in un modulo di iscrizione. È possibile creare un modello con i componenti utilizzabili dagli autori per creare un modulo coerente con gli altri moduli di iscrizione. Quando gli autori utilizzano il modello per creare un modulo adattivo, il nuovo modulo eredita la struttura e i componenti specificati nel modello. L’Editor modelli consente di:

* Aggiungere componenti di intestazione e piè di pagina di un modulo nel livello struttura.
* Fornire il contenuto iniziale del modulo.
* Specifica un tema e invia azioni.

## Utilizzo dei modelli {#working-with-templates}

Per accedere all’editor modelli dal menu Strumenti, vai a **Adobe Experience Manager > Strumenti > Modelli**. In questo caso, i modelli sono organizzati in cartelle abilitate per i modelli modificabili. AEM fornisce una cartella globale per organizzare i modelli. Tuttavia, non è attivato per impostazione predefinita. È possibile richiedere all&#39;amministratore di abilitare la cartella globale o creare una nuova cartella per i modelli. Per ulteriori informazioni sulla creazione delle cartelle, consulta [Cartelle dei modelli](/help/sites-developing/page-templates-editable.md).

Dopo aver toccato per aprire una cartella, verrà visualizzato un pulsante Crea che consente di creare un nuovo modello per i moduli adattivi.

### Creazione di un modello {#create-template}

Dopo aver creato una cartella, apri la cartella ed esegui i seguenti passaggi per creare un modello:

1. Nella console Modello, tocca **Crea** all’interno della cartella creata.
1. Nella sezione Scegli un tipo di modello selezionare **Modello di modulo adattivo** e toccare **Successivo**.

1. Nella sezione Template Details (Dettagli modello) , specifica un Titolo modello e tocca **Crea**.
È possibile fornire una descrizione e una miniatura che è possibile visualizzare quando è possibile selezionare il modello creato al momento della creazione del modulo.

1. Tocca **Fine** per tornare alla console o tocca **Apri** per aprire il modello nell’editor.

### Interfaccia utente dell’editor modelli {#template-editor-ui}

Quando aprite un modello per la modifica, potete vedere i seguenti componenti AEM Editor:

* **Barra degli strumenti della pagina**
Contiene le seguenti opzioni:

   * **Attiva/Disattiva pannello laterale**: Consente di mostrare o nascondere la barra laterale.
   * **Informazioni pagina**: Consente di specificare informazioni quali l’ora di pubblicazione/annullamento della pubblicazione, le miniature, le librerie lato client, i criteri pagina e la libreria lato client della progettazione della pagina.
   * **Emulatore**: Consente di simulare e personalizzare l’aspetto di diversi dispositivi.
   * **Selettore livello:** Consente di modificare il livello.
Puoi scegliere **Struttura** livello o **Contenuto iniziale** strato. Il livello Struttura consente di aggiungere e personalizzare l’intestazione e il piè di pagina. Il livello Contenuto iniziale consente di personalizzare il contenuto del modulo.

   * **Anteprima:** Consente di visualizzare un’anteprima dell’aspetto del modello quando lo si pubblica. È possibile utilizzare Selettore livello e Anteprima per attivare o disattivare le modalità di modifica e anteprima.

* **Barra laterale:** Fornisce i browser Contenuto, Proprietà, Risorse e Componenti .
* **Barra degli strumenti del componente:** Quando selezioni un componente, viene visualizzata una barra degli strumenti che consente di personalizzare il componente.
* **Pagina**: Area in cui aggiungere contenuto per creare il modello.

Vedi [Introduzione alla creazione di moduli adattivi](../../forms/using/introduction-forms-authoring.md) per comprendere l’editor dell’interfaccia utente touch.

### Modifica di un modello {#editing-a-template}

Un modello di modulo adattivo viene creato utilizzando due livelli:

* Struttura
* Contenuto iniziale

Il selettore livello è disponibile accanto all’opzione Anteprima nell’angolo superiore destro dello schermo.

### Struttura {#structure}

Quando si seleziona il livello struttura nell’Editor modelli, è possibile visualizzare i contenitori layout sopra e sotto il contenitore Modulo adattivo. Gli autori possono utilizzare questi contenitori layout per intestazione e piè di pagina. È possibile aggiungere, modificare o personalizzare l’intestazione e il piè di pagina. Trascina il componente Intestazione modulo adattiva nel contenitore di layout sopra il contenitore Modulo adattivo per personalizzare l’intestazione del modello. Trascina il componente Piè di pagina modulo adattivo nel contenitore di layout sotto il contenitore Modulo adattivo per personalizzare il piè di pagina del modello.

![Contenitore di layout nel livello struttura](assets/header-layer-selector.png)

Contenitori di layout nel livello struttura

**A.** Contenitore di layout per componente Intestazione **B.** Contenitore di layout per componente Piè di pagina

Trascina il componente Intestazione modulo adattivo nel contenitore di layout sopra il contenitore Modulo adattivo . Dopo aver aggiunto il componente, puoi specificarne le proprietà che consentono di aggiungere un logo e il relativo titolo.

Allo stesso modo, quando trascini il componente piè di pagina nel contenitore di layout sotto il contenitore Modulo adattivo, puoi fornire le informazioni sul copyright e i dettagli aziendali.

![Intestazione e piè di pagina aggiunti nel livello Struttura](assets/header-and-footer.png)

Intestazione e piè di pagina aggiunti nel livello Struttura

#### Blocco/sblocco dei componenti nel livello struttura {#locking-unlocking-components-in-the-structure-layer}

Quando modificate il modello con il livello struttura selezionato, potete sbloccare l’intestazione e il piè di pagina del modello. Se un componente viene sbloccato nel modello, gli autori dei moduli possono modificare il componente nel modulo adattivo che utilizza il modello. Il blocco di un componente impedisce agli autori di moduli di modificarlo nel modulo adattivo. L’opzione Blocca è disponibile nella barra degli strumenti del componente.

Ad esempio, puoi aggiungere il componente di intestazione nel modello. Quando selezioni il componente, puoi vedere un’opzione Blocca nella barra degli strumenti del componente. In genere, l’intestazione include il nome e il logo della società e non si desidera che gli autori dei moduli modifichino il logo e l’intestazione di un modello. In un modulo adattivo creato utilizzando il modello con il componente intestazione bloccato, gli autori dei moduli non possono modificare il logo e il nome dell’azienda.

>[!NOTE]
>
>Non è consigliabile bloccare o sbloccare singolarmente l’immagine o il logo nel componente intestazione. Puoi sbloccare il componente intestazione.

### Contenuto iniziale {#initial-content}

Quando l’opzione Contenuto iniziale è selezionata, il contenitore Modulo adattivo del modello si apre come un modulo adattivo per la modifica. Come per la creazione di un modulo adattivo, è possibile specificare le impostazioni iniziali, ad esempio la selezione di un tema e l’invio di azioni.

Gli autori dei moduli lo utilizzano come base per creare un modulo. La struttura del flusso di contenuto è specificata nel livello Contenuto iniziale del modello. Per passare alla modifica del contenuto iniziale del modello di modulo, prima di visualizzare l’anteprima nella barra degli strumenti della pagina, toccare ![elenco a discesa canvas](assets/canvas-drop-down.png) **> Contenuto iniziale**.
![Livello di contenuto iniziale nell’Editor modelli](assets/initial-content-layer.png)

Livello Contenuto iniziale nell’Editor modelli che mostra il contenitore Modulo adattivo selezionato per specificare le proprietà.

![contenuto iniziale](assets/initial-content-layer-1.png)

Nel livello Contenuto iniziale è possibile creare il modello di modulo adattivo utilizzato dagli autori come base. La creazione di un modello è simile alla creazione di un modulo e le opzioni disponibili sono disponibili nella barra laterale. Sidebar fornisce browser per contenuti, proprietà, risorse e componenti.

Vedi [Barra laterale](../../forms/using/introduction-forms-authoring.md#sidebar).

>[!NOTE]
>
>Quando si seleziona Archivia contenuto o Memorizza PDF come azione di invio, si ottiene un&#39;opzione per specificare il percorso di archiviazione. Se si specifica il percorso nel modello, tutti i moduli creati da esso avranno lo stesso percorso. È possibile specificare il percorso di archiviazione corretto oppure assicurarsi che gli autori dei moduli lo aggiornino per evitare che i dati vengano memorizzati nello stesso percorso da ogni modulo.

#### Creazione di un modello di modulo adattivo con schede e pannelli  {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Ad esempio, se desideri creare un modello con le seguenti schede:

* Informazioni generali
* Informazioni professionali

È stato aggiunto un logo, un titolo e un piè di pagina nel livello struttura. Bloccare l’intestazione e il piè di pagina per impedire agli autori di moduli di modificarli quando utilizzano il modello per creare moduli.

Modifica il livello da Struttura a Contenuto iniziale e inizia ad aggiungere contenuto al modulo. Per creare una struttura a schede, aggiungi un pannello secondario nel pannello guideRootPanel del contenitore Modulo adattivo. Per aggiungere un pannello:

* Per aggiungere un pannello, tocca **+** quando si seleziona il pulsante **Trascina qui i componenti** opzione .

* Puoi trascinare il componente Pannello dal browser Componenti nella barra laterale.
* Puoi aggiungere un pannello secondario di `guideRootPanel` dalla barra degli strumenti del componente.

Per creare le schede Informazioni generali e Informazioni professionali , aggiungi due pannelli nel pannello figlio della scheda `guideRootPanel`. Seleziona i pannelli e tocca ![cmppr](assets/cmppr.png) per aprire le proprietà nella barra laterale. Modificare i nomi degli elementi come `general-info` e `professional-info`, e titoli rispettivamente come Informazioni generali e Informazioni professionali. Nella barra laterale, tocca il contenuto per aprire il browser del contenuto. Nella scheda Oggetti modulo, selezionare `guideRootPanel`. Nell’editor, viene selezionato guideRootPanel. Tocca ![cmppr](assets/cmppr.png) nella barra degli strumenti del componente per aprire le relative proprietà. Nel campo Layout pannello selezionare **Schede in alto** e toccare **Fine**. Viene applicata la struttura del modello a schede.

#### Aggiunta di contenuto nelle schede {#adding-content-in-tabs}

![Aggiunta di campi nel modello di modulo adattivo](assets/template-edit-initial-content.png)

Dopo aver aggiunto i pannelli e averli strutturati come schede, puoi aggiungere campi all’interno delle schede. Quando selezioni una scheda nell’editor, puoi visualizzare il **Trascina qui i componenti** opzione . È possibile trascinare componenti quali caselle di testo, elementi di elenco e pulsanti. Puoi trascinare i componenti dal browser Componenti nella barra laterale.

Ogni componente dispone di proprietà che migliorano l’acquisizione e la manipolazione dei dati. Ad esempio, puoi abilitare il **Campo obbligatorio** di un componente. Gli autori possono specificare un messaggio che i clienti visualizzano ignorando la compilazione di un campo obbligatorio. Specifica il messaggio in **Messaggio campo richiesto** proprietà.

Nel modello di esempio, i campi Nome, Numero di telefono e Data di nascita vengono aggiunti nella scheda Informazioni generali. Nella scheda Informazioni professionali, Attualmente impiegato, vengono aggiunti i campi Tipo di impiego, Qualificazione didattica.

Dopo aver aggiunto i campi, puoi aggiungere pulsanti quali Invia e Reimposta.

### Abilitazione del modello {#enabling-the-template}

Quando crei un modello, questo viene aggiunto come bozza. Attiva il modello per utilizzarlo per la creazione di moduli adattivi. Per abilitare un modello:

1. Passa a **Adobe Experience Manager > Strumenti > Modelli**, quindi apri la cartella in cui hai creato il modello.

1. Il modello creato viene contrassegnato come Bozza.
1. Seleziona il modello e tocca **Abilita** nella barra degli strumenti.
Quando si crea un modulo adattivo, è possibile visualizzare i modelli elencati quando viene richiesto di scegliere un modello.

## Importazione o esportazione di un modello {#importing-or-exporting-a-template}

Un modulo funziona con il relativo modello. Quando si scarica un modulo adattivo creato utilizzando un modello personalizzato, il modello non viene scaricato. Quando si importa il modulo in un’altra istanza di AEM Forms, questo viene importato senza il relativo modello. Se un modulo viene importato ma il relativo modello non è disponibile, il modulo non viene sottoposto a rendering. Puoi creare un pacchetto del modello personalizzato da `/conf` nodo in `https://<server>:<port>/crx/packmgr`, e porta nell’istanza di AEM Forms in cui desideri caricare il modulo.

## Creazione di un modulo adattivo utilizzando il modello {#creating-an-adaptive-form-using-the-template}

Dopo aver creato e abilitato un modello, questo è disponibile in Forms Manager quando si crea un modulo adattivo. Per utilizzare un modello e creare un modulo adattivo, consulta [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md).

## Modifica l’opzione di visualizzazione dei modelli predefiniti  {#change-display-option-of-out-of-the-box-templates}

È possibile creare modelli personalizzati per i moduli adattivi per definire la struttura di base e il contenuto iniziale. AEM Forms fornisce inoltre un set di modelli predefiniti per i moduli adattivi. È possibile scegliere di mostrare o nascondere i modelli.

Esegui i seguenti passaggi per mostrare e nascondere i modelli:

1. Accedi all’istanza di authoring di AEM Forms e passa a **Strumenti** > **Operazioni** > **Console web**.

   >[!NOTE]
   >
   >L’URL della console Web AEM è https://&#39;[server]:[porta]&#39;/system/console/configMgr

1. Individua e apri la **Configurazione di FormsManager** impostazioni:

   * Per visualizzare o nascondere il modello di moduli adattivi predefinito, seleziona o deseleziona la **Includi modelli predefiniti AF e AD** opzione .
   * Per visualizzare o nascondere i modelli di modulo adattivo predefiniti aggiunti nelle versioni Forms 6.0 o Forms 6.1 di AEM ma ora obsoleti, seleziona o deseleziona la **Includi modelli AF AEM 6.0** opzione . Se questa opzione è selezionata, per avere effetto è necessario **Includi modelli predefiniti AF e AD** configurazione da abilitare.

1. Fai clic su **Salva**. Vengono modificate le opzioni di visualizzazione per i modelli predefiniti.

## Consigli {#recommendations}

* Quando si modificano le proprietà del modulo nell&#39;editor modelli, non utilizzare la proprietà BindReference.
* Per aggiungere un punto di interruzione, crealo quando crei un modello di modulo adattivo.
Per ulteriori informazioni sui punti di interruzione, vedi [Layout reattivo](/help/sites-authoring/responsive-layout.md).
