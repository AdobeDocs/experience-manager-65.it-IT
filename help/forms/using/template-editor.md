---
title: Modelli di moduli adattivi
seo-title: Modelli di moduli adattivi
description: Creare modelli di modulo adattivi definendo la struttura di base e il contenuto iniziale del modulo utilizzando l'Editor modelli.
seo-description: Creare modelli di modulo adattivi definendo la struttura di base e il contenuto iniziale del modulo utilizzando l'Editor modelli.
uuid: 317ca3ab-f809-49a7-a063-9d0c17a35fe4
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b21a48ba-eccd-4bb5-9b92-3039026ddf2a
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1984'
ht-degree: 0%

---


# Modelli di modulo adattivo{#adaptive-form-templates}

Quando si crea un modulo, è possibile aggiungere campi e componenti per definire la struttura del modulo, il contenuto e le azioni nell&#39;editor. È possibile aggiungere campi e componenti in `guideRootPanel` del contenitore del modulo. Utilizzando l&#39;Editor modelli è possibile creare un modello che contiene la struttura di base e il contenuto iniziale che gli autori possono utilizzare per creare moduli.

Ad esempio, si desidera che tutti gli autori dei moduli dispongano di determinate caselle di testo, pulsanti di navigazione e un pulsante di invio in un modulo di iscrizione. È possibile creare un modello con i componenti che gli autori possono utilizzare per creare un modulo coerente con altri moduli di iscrizione. Quando gli autori utilizzano il modello per creare un modulo adattivo, il nuovo modulo eredita la struttura e i componenti specificati nel modello. Editor modelli consente di:

* Aggiungere componenti di intestazione e piè di pagina di un modulo nel livello struttura.
* Fornire il contenuto iniziale per il modulo.
* Specificate un tema e inviate le azioni.

## Utilizzo dei modelli {#working-with-templates}

È possibile accedere all&#39;editor modelli dal menu Strumenti scegliendo **Adobe Experience Manager > Strumenti > Modelli**. In questo caso, i modelli sono organizzati in cartelle abilitate per i modelli modificabili. AEM una cartella globale per organizzare i modelli. Tuttavia, per impostazione predefinita non è attivato. Potete richiedere all’amministratore di abilitare la cartella globale o di creare una nuova cartella per i modelli. Per ulteriori informazioni sulla creazione di cartelle, vedere [Cartelle modello](/help/sites-developing/page-templates-editable.md).

Toccando per aprire una cartella, è disponibile un pulsante Crea che consente di creare un nuovo modello per i moduli adattivi.

### Creazione di un modello {#create-template}

Dopo aver creato una cartella, aprite la cartella ed eseguite i seguenti passaggi per creare un modello:

1. Nella console Modello, toccare **Crea** all’interno della cartella creata.
1. Nella sezione Selezionare un tipo di modello, selezionare **Modello di modulo adattivo** e toccare **Avanti**.

1. Nella sezione Template Details (Dettagli modello), fornite un Titolo modello e toccate **Create**.
È possibile fornire una descrizione e una miniatura che consentano di vedere quando è possibile selezionare il modello creato al momento della creazione del modulo.

1. Toccate **Fine** per tornare alla console oppure toccate **Apri** per aprire il modello nell&#39;editor.

### Interfaccia utente dell&#39;editor modelli {#template-editor-ui}

Quando aprite un modello per la modifica, potete vedere i seguenti componenti dell’editor AEM:

* **Barra**
degli strumenti PaginaContiene le opzioni seguenti:

   * **Attiva/Disattiva pannello** laterale: Consente di mostrare o nascondere la barra laterale.
   * **Informazioni** pagina: Consente di specificare informazioni quali l’ora di pubblicazione/annullamento della pubblicazione, le miniature, le librerie lato client, i criteri pagina e la libreria lato client della progettazione della pagina.
   * **Emulatore**: Consente di simulare e personalizzare l’aspetto di diversi dispositivi.
   * **Selettore livello:** consente di modificare il livello.
Potete scegliere il livello **Struttura** o **Contenuto iniziale**. Il livello Struttura consente di aggiungere e personalizzare l’intestazione e il piè di pagina. Il livello Contenuto iniziale consente di personalizzare il contenuto del modulo.

   * **Anteprima:** consente di visualizzare un’anteprima dell’aspetto del modello al momento della pubblicazione. Potete usare Selettore livello e Anteprima per alternare le modalità di modifica e anteprima.

* **Barra laterale:** fornisce i browser Contenuto, Proprietà, Risorse e Componenti.
* **Barra degli strumenti del componente:** quando si seleziona un componente, viene visualizzata una barra degli strumenti che consente di personalizzare il componente.
* **Pagina**: Area in cui aggiungere il contenuto per creare il modello.

Per informazioni sull&#39;editor dell&#39;interfaccia touch, vedere [Introduzione alla creazione di moduli adattivi](../../forms/using/introduction-forms-authoring.md).

### Modifica di un modello {#editing-a-template}

Un modello di modulo adattivo viene creato utilizzando due livelli:

* Struttura
* Contenuto iniziale

Il selettore del livello è disponibile accanto all’opzione Anteprima nell’angolo superiore destro dello schermo.

### Struttura {#structure}

Quando si seleziona il livello struttura nell&#39;Editor modelli, è possibile vedere i contenitori di layout sopra e sotto il contenitore del modulo adattivo. Gli autori possono utilizzare questi contenitori di layout per intestazione e piè di pagina. Potete aggiungere, modificare o personalizzare l’intestazione e il piè di pagina. Trascinare il componente Intestazione modulo adattiva nel contenitore di layout sopra il contenitore Modulo adattivo per personalizzare l’intestazione del modello. Trascinare il componente Piè di pagina modulo adattivo nel contenitore di layout sotto il contenitore Modulo adattivo per personalizzare il piè di pagina del modello.

![Contenitore di layout nel livello struttura](assets/header-layer-selector.png)

Contenitori di layout nel livello struttura

**A.Contenitore** di layout per il componente Intestazione  **B.Contenitore di** layout per il componente Piè di pagina

Trascinare il componente Intestazione modulo adattiva nel contenitore di layout sopra il contenitore Modulo adattivo. Dopo aver aggiunto il componente, potete specificarne le proprietà che consentono di aggiungere un logo e il relativo titolo.

Allo stesso modo, quando trascinate il componente piè di pagina nel contenitore di layout sotto il contenitore per moduli adattivi, potete fornire le informazioni sul copyright e i dettagli aziendali.

![Intestazione e piè di pagina aggiunti nel livello Struttura](assets/header-and-footer.png)

Intestazione e piè di pagina aggiunti nel livello Struttura

#### Blocco/sblocco dei componenti nel livello struttura {#locking-unlocking-components-in-the-structure-layer}

Quando modificate il modello con il livello struttura selezionato, potete sbloccare l’intestazione e il piè di pagina del modello. Se un componente non è bloccato nel modello, gli autori dei moduli possono modificare il componente nel modulo adattivo che utilizza il modello. Il blocco di un componente impedisce agli autori del modulo di modificarlo nel modulo adattivo. L’opzione Blocca è disponibile nella barra degli strumenti del componente.

Ad esempio, potete aggiungere il componente intestazione nel modello. Quando selezionate il componente, l’opzione Blocca è disponibile nella barra degli strumenti del componente. In genere, l’intestazione include il nome della società e il logo e non si desidera che gli autori dei moduli modifichino il logo e l’intestazione di un modello. In un modulo adattivo creato utilizzando il modello con il componente intestazione bloccato, gli autori dei moduli non possono modificare il logo e il nome della società.

>[!NOTE]
>
>Non è consigliabile bloccare o sbloccare singolarmente l’immagine o il logo nel componente intestazione. Potete sbloccare il componente dell’intestazione.

### Contenuto iniziale {#initial-content}

Quando l&#39;opzione Contenuto iniziale è selezionata, il contenitore modulo adattivo del modello si apre come un modulo adattivo per la modifica. Come per la creazione di un modulo adattivo, è possibile specificare le impostazioni iniziali, ad esempio la selezione di un tema e l&#39;invio di azioni.

Gli autori dei moduli la utilizzano come base per creare un modulo. La struttura del flusso di contenuto è specificata nel livello Contenuto iniziale del modello. Per passare alla modifica del contenuto iniziale del modello di modulo, prima di visualizzare l&#39;anteprima nella barra degli strumenti della pagina, toccare l&#39;elenco a discesa ![canvas](assets/canvas-drop-down.png) **> Contenuto iniziale**.
![Livello contenuto iniziale nell&#39;Editor modelli](assets/initial-content-layer.png)

Livello contenuto iniziale nell&#39;Editor modelli che mostra il contenitore modulo adattivo selezionato per specificare le proprietà.

![contenuto iniziale](assets/initial-content-layer-1.png)

Nel livello Contenuto iniziale, è possibile creare il modello di modulo adattivo utilizzato dagli autori come base. L’authoring di un modello è simile all’authoring di un modulo e le opzioni sono disponibili nella barra laterale. La barra laterale fornisce browser di contenuti, proprietà, risorse e componenti.

Vedere [Barra laterale](../../forms/using/introduction-forms-authoring.md#sidebar).

>[!NOTE]
>
>Quando si seleziona Archivia contenuto o Memorizza PDF come azione di invio, è possibile specificare il percorso di archiviazione. Se si specifica il percorso nel modello, tutti i moduli creati da esso avranno lo stesso percorso. È possibile specificare il percorso di memorizzazione corretto o assicurarsi che gli autori dei moduli lo aggiornino per evitare che i dati di ogni modulo vengano memorizzati nella stessa posizione.

#### Creazione di un modello di modulo adattivo con schede e pannelli  {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Ad esempio, potete creare un modello con le seguenti schede:

* Informazioni generali
* Informazioni professionali

È stato aggiunto un logo, un titolo e un piè di pagina al livello struttura. Bloccare l&#39;intestazione e il piè di pagina per impedire agli autori di modificarli quando utilizzano il modello per creare moduli.

Modificate il livello da Struttura a Contenuto iniziale e iniziate ad aggiungere contenuto al modulo. Per creare una struttura a schede, aggiungere un pannello secondario nel pannello guideRoot del contenitore Modulo adattivo. Per aggiungere un pannello:

* Per aggiungere un pannello, toccate il pulsante **+** quando selezionate l&#39;opzione **Trascinate qui i componenti**.

* Potete trascinare il componente Pannello dal Browser componenti nella barra laterale.
* È possibile aggiungere un pannello secondario della `guideRootPanel` dalla barra degli strumenti del componente.

Per creare le schede Informazioni generali e Informazioni professionali, aggiungete due pannelli nel pannello secondario di `guideRootPanel`. Selezionate i pannelli e toccate ![cmppr](assets/cmppr.png) per aprire le proprietà nella barra laterale. Modificate i nomi degli elementi come `general-info` e `professional-info`, e i titoli rispettivamente come Informazioni generali e Informazioni professionali. Nella barra laterale, toccate il contenuto per aprire il browser del contenuto. Nella scheda Oggetti modulo, selezionare `guideRootPanel`. Nell’editor, è selezionato guideRootPanel. Toccate ![cmppr](assets/cmppr.png) nella barra degli strumenti del componente per aprirne le proprietà. Nel campo Layout pannello, selezionate **Tabulazioni in alto** e toccate **Fine**. Viene applicata la struttura del modello a schede.

#### Aggiunta di contenuto alle schede {#adding-content-in-tabs}

![Aggiunta di campi nel modello di modulo adattivo](assets/template-edit-initial-content.png)

Dopo aver aggiunto i pannelli e averli strutturati come schede, potete aggiungere campi all’interno delle schede. Quando si seleziona una scheda nell&#39;editor, è possibile visualizzare l&#39;opzione **Trascina qui i componenti**. È possibile trascinare componenti come caselle di testo, elementi elenco e pulsanti. Puoi trascinare componenti dal browser Componenti nella barra laterale.

Ciascun componente dispone di proprietà che migliorano l’acquisizione e la manipolazione dei dati. Ad esempio, è possibile abilitare la proprietà **Campo obbligatorio** di un componente. Gli autori possono specificare un messaggio che i clienti potranno visualizzare quando saltano la compilazione di un campo obbligatorio. Specificare il messaggio nella proprietà **Messaggio campo obbligatorio**.

Nel modello di esempio, i campi Nome, Numero di telefono e Data di nascita vengono aggiunti nella scheda Informazioni generali. Nella scheda Informazioni professionali, Attualmente in uso, vengono aggiunti i campi Tipo di impiego, Qualificazione per istruzione.

Dopo aver aggiunto i campi, potete aggiungere pulsanti quali Invia e Ripristina.

### Abilitazione del modello {#enabling-the-template}

Quando create un modello, questo viene aggiunto come bozza. Abilitare il modello a utilizzarlo per la creazione di moduli adattivi. Per abilitare un modello:

1. Andate su **Adobe Experience Manager > Strumenti > Modelli** e aprite la cartella in cui avete creato il modello.

1. Il modello creato è contrassegnato come Bozza.
1. Selezionate il modello e toccate **Abilita** nella barra degli strumenti.
Quando si crea un modulo adattivo, è possibile visualizzare il modello elencato quando viene richiesto di scegliere un modello.

## Importazione o esportazione di un modello {#importing-or-exporting-a-template}

Un modulo funziona con il relativo modello. Quando si scarica un modulo adattivo creato utilizzando un modello personalizzato, il modello non viene scaricato. Quando si importa il modulo in un&#39;altra istanza  AEM Forms, questo viene importato senza il relativo modello. Se un modulo viene importato ma il suo modello non è disponibile, non viene eseguito il rendering. È possibile creare un pacchetto del modello personalizzato dal nodo `/conf` in `https://<server>:<port>/crx/packmgr` e portarlo nell&#39;istanza AEM Forms  in cui si desidera caricare il modulo.

## Creazione di un modulo adattivo utilizzando il modello {#creating-an-adaptive-form-using-the-template}

Dopo aver creato e attivato un modello, questo sarà disponibile in Forms Manager quando si crea un modulo adattivo. Per utilizzare un modello e creare un modulo adattivo, vedere [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md).

## Modifica dell&#39;opzione di visualizzazione dei modelli predefiniti {#change-display-option-of-out-of-the-box-templates}

È possibile creare modelli personalizzati per i moduli adattivi per definire la struttura di base e il contenuto iniziale.  AEM Forms fornisce inoltre un set di modelli predefiniti per i moduli adattivi. Potete scegliere di mostrare o nascondere i modelli.

Per visualizzare e nascondere i modelli, effettuate le seguenti operazioni:

1. Accedete  istanza di creazione AEM Forms e andate a **Strumenti** > **Operazioni** > **Console Web**.

   >[!NOTE]
   >
   >L&#39;URL di AEM console Web è https://&#39;[server]:[porta]&#39;/system/console/configMgr

1. Individuare e aprire le impostazioni **Configurazione FormsManager**:

   * Per visualizzare o nascondere il modello di moduli adattivi, selezionare o deselezionare l&#39;opzione **Includi fuori dalla casella Modelli AF e AD**.
   * Per visualizzare o nascondere i modelli di modulo adattivo inclusi nelle versioni di Forms AEM 6.0 Forms o AEM 6.1 ma ora non più disponibili, selezionare o deselezionare l&#39;opzione **Includi AEM 6.0 AF Templates**. Se questa opzione è selezionata, per avere effetto, è necessario abilitare la configurazione **Includi modelli AF e AD**.

1. Fai clic su **Salva**. Le opzioni di visualizzazione per i modelli forniti vengono modificate.

## Consigli {#recommendations}

* Quando si modificano le proprietà del modulo nell&#39;editor modelli, non utilizzare la proprietà BindReference.
* Se si desidera aggiungere un punto di interruzione, crearlo al momento della creazione di un modello di modulo adattivo.
Per ulteriori informazioni sui punti di interruzione, vedere [Layout reattivo](/help/sites-authoring/responsive-layout.md).

