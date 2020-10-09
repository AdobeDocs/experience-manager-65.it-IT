---
title: Modelli di risorse
description: Scopri i modelli delle risorse [!DNL Adobe Experience Manager Assets] e come utilizzare i modelli delle risorse per creare materiale collaterale di marketing.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f9f745369ba0fe242dea1e5a5e5af0b8263b1ec0
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 1%

---


# Asset templates {#asset-templates}

I modelli di risorse sono una classe speciale di risorse che semplificano la ridefinizione rapida dei contenuti visivamente avanzati per i supporti digitali e di stampa. Un modello di risorsa include due parti: la sezione relativa ai messaggi fissi e la sezione modificabile. La sezione relativa ai messaggi fissi può contenere contenuti proprietari, ad esempio il logo del marchio e le informazioni sul copyright, che sono disattivati per la modifica. La sezione modificabile può contenere contenuti visivi e testuali in campi che possono essere modificati per personalizzare i messaggi.

La flessibilità di apportare modifiche limitate e la protezione del digital signage rende i modelli di risorse ideali per l’adattamento e la distribuzione rapida dei contenuti come artefatti di contenuto per varie funzioni. La ridefinizione dei contenuti consente di ridurre i costi per la gestione dei canali digitali e per la stampa e di offrire esperienze complete e coerenti su questi canali.

Gli esperti di marketing possono archiviare e gestire i modelli all&#39;interno [!DNL Experience Manager Assets] e utilizzare un singolo modello di base per creare più esperienze di stampa personalizzate con facilità. Puoi creare diversi tipi di materiale collaterale di marketing, inclusi brochure, volantini, cartoline, biglietti da visita e così via, per trasmettere in modo chiaro il messaggio di marketing ai clienti. È inoltre possibile assemblare output di stampa di più pagine da uscite di stampa esistenti o nuove. Soprattutto, è possibile distribuire simultaneamente esperienze digitali e di stampa con facilità, offrendo agli utenti un&#39;esperienza coerente e integrata.

Anche se i modelli di risorse sono principalmente [!DNL Adobe InDesign] file, l’esperienza acquisita non [!DNL Adobe InDesign] rappresenta una barriera alla creazione di artefatti stellari. Non è necessario mappare i campi del [!DNL Adobe InDesign] modello con i campi del prodotto che altrimenti sarebbero necessari per la creazione di cataloghi. Potete modificare i modelli in modalità WYSIWYG direttamente sull&#39;interfaccia Web. Tuttavia, per [!DNL Adobe InDesign] elaborare le modifiche dovete prima configurare [!DNL Experience Manager Assets] per l’integrazione con [!DNL Adobe InDesign Server].

La possibilità di modificare [!DNL Adobe InDesign] i modelli dall&#39;interfaccia Web favorisce una maggiore collaborazione tra il personale creativo e di marketing. L&#39;aumento della velocità dei contenuti riduce il time-to-market per le garanzie di marketing.

Con i modelli di risorse potete ottenere quanto segue:

* Modificare i campi dei modelli modificabili dall&#39;interfaccia Web.
* Controllare lo stile di base del testo, ad esempio dimensione del font, stile e tipo a livello di tag.
* Cambiate le immagini all’interno del modello utilizzando il selettore dei contenuti.
* Anteprima delle modifiche apportate al modello.
* Unisci più file modello per creare un artefatto con più pagine.

Quando scegli un modello per la tua offerta, [!DNL Experience Manager Assets] crea una copia del modello che puoi modificare. Il modello originale viene mantenuto, in modo da garantire che il digital signage rimanga intatto e possa essere riutilizzato per garantire la coerenza del marchio.

Potete esportare il file aggiornato all’interno della cartella principale nei formati INDD, PDF o JPG. È inoltre possibile scaricare l&#39;output in questi formati nel file system locale.

## Creare una garanzia {#creating-a-collateral}

Considerate uno scenario in cui desiderate creare materiale collaterale stampabile digitale, come brochure, volantini e annunci pubblicitari per una campagna imminente e condividetelo con gli outlet store a livello globale. La creazione di materiale collaterale basato su un modello consente di offrire un&#39;esperienza cliente unificata tra i canali. I designer possono creare i modelli delle campagne (pagina singola o pagina multipla) utilizzando una soluzione creativa, ad esempio [!DNL InDesign] e caricando i modelli [!DNL Experience Manager Assets] per voi. Prima di creare una garanzia collaterale, potete caricare e rendere disponibili in [!DNL Experience Manager] anticipo uno o più modelli INDD.

1. Nell’ [!DNL Experience Manager] interfaccia, fai clic su [!UICONTROL Risorse].

1. Tra le opzioni, scegliete **[!UICONTROL Modelli]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Fate clic su **[!UICONTROL Crea]**, quindi scegliete dal menu la risorsa da creare. Ad esempio, scegliete **[!UICONTROL Brochure]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Accertatevi che uno o più modelli INDD siano caricati e disponibili [!DNL Experience Manager] in anticipo. Scegliete un modello per la brochure e fate clic su **[!UICONTROL Avanti]**.
1. Specificate un nome e una descrizione facoltativa per la brochure.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Facoltativo) Fate clic su **[!UICONTROL Tag]** e selezionate uno o più tag per la brochure. Fate clic su **[!UICONTROL Conferma]** per confermare la selezione.
1. Fai clic su **[!UICONTROL Crea]**. Una finestra di dialogo conferma la creazione di una nuova brochure. Fate clic su **[!UICONTROL Apri]** per aprire la brochure in modalità di modifica.

   <!--![chlimage_1-106](assets/.png) -->

   In alternativa, chiudete la finestra di dialogo e individuate la cartella nella pagina Modelli con cui avete iniziato a visualizzare la brochure creata. Il tipo di materiale collaterale viene visualizzato sulla relativa miniatura nella vista a schede. Ad esempio, in questo caso, la parola [!UICONTROL Brochure] viene visualizzata sulla miniatura.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Modificare un materiale collaterale {#editing-a-collateral}

È possibile modificare un materiale collaterale immediatamente dopo averlo creato. In alternativa, potete aprirlo dalla pagina [!UICONTROL Modelli] o dalla pagina della risorsa.

1. Per aprire il materiale collaterale per la modifica, effettuate una delle seguenti operazioni:

   * Aprire il materiale collaterale (in questo caso la brochure) creato nel passaggio 7 di [Creare un materiale collaterale](/help/assets/asset-templates.md#creating-a-collateral).
   * Dalla pagina Modelli, individuate la cartella in cui avete creato la garanzia collaterale e fate clic sull&#39;azione rapida [!UICONTROL Modifica] sulla miniatura di una garanzia reale.
   * Nella pagina della risorsa per il materiale collaterale, fate clic su **[!UICONTROL Modifica]** nella barra degli strumenti.
   * Select the collateral and click **[!UICONTROL Edit]** from the toolbar.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   A sinistra della pagina vengono visualizzati il cercatore di risorse e l’editor di testo. L&#39;editor di testo è aperto per impostazione predefinita.

   È possibile utilizzare l&#39;editor di testo per modificare il testo che si desidera visualizzare nel campo di testo. Potete modificare la dimensione del font, lo stile, il colore e il tipo a livello di tag.

   Utilizzando il tool di ricerca delle risorse, potete cercare o individuare immagini all’interno [!DNL Experience Manager Assets] e sostituire le immagini modificabili nel modello con immagini di vostra scelta.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   I modificabili sono visualizzati a destra. Affinché un campo possa essere modificato in [!DNL Experience Manager Assets], il campo corrispondente nel modello deve essere contrassegnato in [!DNL InDesign]. In altre parole, devono essere contrassegnati come modificabili in [!DNL InDesign].

   >[!NOTE]
   >
   >Assicuratevi che la [!DNL Experience Manager] distribuzione sia integrata con un [!DNL InDesign Server] sistema per consentire [!DNL Experience Manager Assets] di estrarre i dati dal [!DNL InDesign] modello e renderlo disponibile per la modifica. Per informazioni dettagliate, consultate [Integrazione  risorse di Experience Manager con  InDesign Server](/help/assets/indesign.md).

1. Per modificare il testo in un campo modificabile, fare clic sul campo di testo nell&#39;elenco dei campi modificabili e modificare il testo nel campo.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   È possibile modificare le proprietà del testo, ad esempio stile del font, colore e dimensione utilizzando le opzioni disponibili.

1. Fate clic su **[!UICONTROL Anteprima]** per visualizzare l’anteprima delle modifiche di testo.

1. Per sostituire un’immagine, fate clic sul **[!UICONTROL collegamento Asset Finder]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. Selezionate il campo immagine dall’elenco dei campi modificabili, quindi trascinate l’immagine desiderata dal selettore delle risorse al campo modificabile.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   Potete anche cercare le immagini usando parole chiave, tag e in base al loro stato di pubblicazione. Potete sfogliare l’ [!DNL Experience Manager Assets] archivio e individuare la posizione dell’immagine desiderata.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Fate clic su **[!UICONTROL Anteprima]** per visualizzare l’anteprima dell’immagine.
1. Per modificare una pagina specifica in un materiale collaterale composto da più pagine, utilizzate il navigatore pagina nella parte inferiore.

1. Fate clic su **[!UICONTROL Anteprima]** sulla barra degli strumenti per visualizzare in anteprima tutte le modifiche. Fate clic su **[!UICONTROL Fine]** per salvare le modifiche apportate al materiale collaterale.

   >[!NOTE]
   >
   >Le opzioni Anteprima e Fine sono abilitate solo quando i campi immagine modificabili all’interno della risorsa collaterale non presentano icone mancanti. Se vi sono icone mancanti nella risorsa collaterale, è perché non [!DNL Experience Manager] è possibile risolvere le immagini nel [!DNL InDesign] modello. In genere [!DNL Experience Manager] non è in grado di risolvere le immagini nei seguenti casi:
   >
   >* Le immagini non sono incorporate nel [!DNL InDesign] modello sottostante.
   >* Le immagini sono collegate dal file system locale.

   >
   >Per consentire [!DNL Experience Manager] di risolvere le immagini, effettuate le seguenti operazioni:
   >
   >* Incorporare le immagini durante la creazione di [!DNL InDesign] modelli (consultate [I collegamenti e gli elementi grafici](https://helpx.adobe.com/indesign/using/graphics-links.html)incorporati).
   >* Passate [!DNL Experience Manager] al file system locale e mappate le icone mancanti con le risorse esistenti in [!DNL Experience Manager].

   >
   >Per ulteriori informazioni sull&#39;uso dei [!DNL InDesign] documenti, vedere [Best practice per l&#39;utilizzo di documenti InDesign  in  Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Per generare una rappresentazione PDF per la brochure, selezionate l’opzione  Acrobat nella finestra di dialogo, quindi fate clic su **[!UICONTROL Continua]**.
1. Il materiale collaterale viene creato nella cartella con cui avete iniziato. Per visualizzare i rendering, aprite il materiale collaterale e scegliete **[!UICONTROL Rendering]** dall’elenco di navigazione globale.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Fare clic sulla rappresentazione PDF dall&#39;elenco delle rappresentazioni per scaricare il file PDF. Aprire il file PDF per esaminare le risorse.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Unisci materiale collaterale {#merge-collateral}

1. Nell’ [!DNL Experience Manager] interfaccia, fate clic su [!UICONTROL Risorse] nella pagina di navigazione.

1. Tra le opzioni, scegliete **[!UICONTROL Modelli]**.

1. Fate clic su **[!UICONTROL Crea]** e scegliete **[!UICONTROL Unisci]** dal menu.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. Dalla pagina Unione  modelli, fate clic su **[!UICONTROL Unisci]** per ![aggiungere risorse](assets/do-not-localize/assets_add_icon.png).

1. Andate alla posizione del materiale collaterale da unire e fate clic sulle miniature del materiale collaterale da unire per selezionarlo.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Potete anche cercare i modelli dalla casella di ricerca Omnice.

   Potete sfogliare la [!DNL Experience Manager Assets] directory archivio o le raccolte, individuare la posizione dei modelli desiderati e selezionarli per l&#39;unione.

   Potete applicare vari filtri per cercare nei modelli desiderati. Ad esempio, potete cercare i modelli in base al tipo di file o ai tag.

1. Click **[!UICONTROL Next]** from the toolbar.
1. Nella schermata **[!UICONTROL Anteprima e riordina]** , se necessario ridisponete i modelli e visualizzate l’anteprima della selezione di modelli da unire. Quindi fate clic su **[!UICONTROL Avanti]** nella barra degli strumenti.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. Nella schermata [!UICONTROL Configura modello] , specificate un nome per il materiale collaterale. Facoltativamente, potete specificare i tag desiderati. Se si desidera esportare l&#39;output in formato PDF, selezionare **[!UICONTROL Acrobat (.PDF)]**. Per impostazione predefinita, il materiale collaterale viene esportato in formato JPG e [!DNL InDesign] format. Per modificare la miniatura di visualizzazione per le risorse di più pagine collaterali, fate clic su **[!UICONTROL Cambia miniatura]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Fate clic su **[!UICONTROL Salva]** , quindi su **[!UICONTROL OK]** nella finestra di dialogo per chiudere la finestra di dialogo. Il materiale collaterale a più pagine viene creato nella cartella con cui avete iniziato.

   >[!NOTE]
   >
   >Non è possibile modificare un materiale collaterale unito in un secondo momento o utilizzarlo per creare altre risorse.

## Best practice e limitazioni {#best-practices-limitations-tips}

* L’ [!DNL InDesign] editor in [!DNL Experience Manager] funziona a livello di tag e tutto il testo all’interno di un singolo tag viene considerato come una singola entità. Per mantenere la formattazione del testo e gli stili durante la modifica, assegnate separatamente i tag a ciascun paragrafo (o testo con stili diversi).
