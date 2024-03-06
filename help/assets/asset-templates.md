---
title: Modelli di risorse
description: Scopri i modelli di risorse in [!DNL Adobe Experience Manager Assets] e come utilizzare i modelli di risorse per creare materiale promozionale di marketing.
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 1%

---

# Modelli di risorse {#asset-templates}

I modelli di risorse sono una classe speciale di risorse che facilita la ridefinizione rapida dei contenuti con effetti visivi avanzati per i supporti digitali e di stampa. Un modello di risorsa include due parti, la sezione messaggi fissi e la sezione modificabile. La sezione dei messaggi fissi può contenere contenuti proprietari, ad esempio il logo del marchio e informazioni sul copyright, che sono disabilitati per la modifica. La sezione modificabile può contenere contenuti visivi e testuali in campi che possono essere modificati per personalizzare la messaggistica.

La flessibilità di apportare modifiche limitate, pur proteggendo il digital signage globale, rende i modelli di risorse ideali per adattare e distribuire rapidamente i contenuti come artefatti per varie funzioni. I contenuti riproposti consentono di ridurre i costi di gestione dei canali di stampa e digitali e di offrire esperienze olistiche e coerenti su questi canali.

In qualità di addetto al marketing, puoi archiviare e gestire modelli in [!DNL Experience Manager Assets] e utilizza un singolo modello di base per creare con facilità più esperienze di stampa personalizzate. Puoi creare vari tipi di materiale promozionale di marketing, tra cui opuscoli, volantini, cartoline, biglietti da visita e così via, per trasmettere in modo lucido il messaggio di marketing ai clienti. È inoltre possibile assemblare output di stampa multipagina da output di stampa nuovi o esistenti. Soprattutto, puoi fornire simultaneamente esperienze digitali e di stampa con facilità, per fornire agli utenti un’esperienza coerente e integrata.

Mentre i modelli di risorse sono per lo più [!DNL Adobe InDesign] file, esperienza in [!DNL Adobe InDesign] non è una barriera per la creazione di artefatti stellari. Non è necessario mappare i campi del [!DNL Adobe InDesign] con i campi dei prodotti che altrimenti sarebbero necessari per la creazione dei cataloghi. È possibile modificare i modelli in modalità WYSIWYG direttamente sull’interfaccia web. Tuttavia, per [!DNL Adobe InDesign] per elaborare le modifiche, devi prima configurare [!DNL Experience Manager Assets] da integrare con [!DNL Adobe InDesign Server].

Possibilità di modificare [!DNL Adobe InDesign] I modelli dall’interfaccia web consentono di migliorare la collaborazione tra il personale creativo e di marketing. La maggiore velocità dei contenuti riduce il time-to-market dei materiali di marketing.

Con i modelli di risorse puoi ottenere quanto segue:

* Modifica i campi modello modificabili dall’interfaccia web.
* Controlla lo stile di base del testo, ad esempio la dimensione, lo stile e il tipo di carattere a livello di tag.
* Modifica le immagini all’interno del modello utilizzando il Selettore contenuto.
* Visualizzare in anteprima le modifiche apportate ai modelli.
* Unisci più file modello per creare un artefatto con più pagine.

Quando scegli un modello per il materiale promozionale, [!DNL Experience Manager Assets] crea una copia del modello che è possibile modificare. Il modello originale è preservato: il digital signage rimane intatto e può essere riutilizzato per garantire la coerenza del marchio.

Puoi esportare il file aggiornato all’interno della cartella principale in formati INDD, PDF o JPG. È inoltre possibile scaricare l&#39;output in questi formati nel file system locale.

## Creare un pezzo di materiale promozionale {#creating-a-collateral}

Considera uno scenario in cui desideri creare materiale collaterale digitale stampabile, ad esempio brochure, volantini e annunci per una prossima campagna e condividerlo con i punti vendita di tutto il mondo. La creazione di materiale collaterale basato su un modello consente di fornire ai clienti un’esperienza unificata su tutti i canali. I designer possono creare i modelli di campagna (a pagina singola o multipagina) utilizzando una soluzione creativa, ad esempio [!DNL InDesign] e caricare i modelli in [!DNL Experience Manager Assets] per te. Prima di creare un materiale promozionale, carica e rendi disponibili uno o più modelli INDD in [!DNL Experience Manager] in anticipo.

1. In [!DNL Experience Manager] interfaccia, seleziona [!UICONTROL Risorse].

1. Tra le opzioni, scegli **[!UICONTROL Modelli]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Seleziona **[!UICONTROL Crea]**, quindi scegliere il materiale promozionale da creare dal menu. Ad esempio, scegli **[!UICONTROL Brochure]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Puoi caricare e rendere disponibili uno o più modelli INDD in [!DNL Experience Manager] in anticipo. Scegliere un modello per la brochure e fare clic su **[!UICONTROL Successivo]**.
1. Specificare un nome e una descrizione facoltativa per la brochure.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Facoltativo) Fai clic su **[!UICONTROL Tag]** e selezionare uno o più tag per la brochure. Clic **[!UICONTROL Conferma]** per confermare la selezione.
1. Fai clic su **[!UICONTROL Crea]**. Una finestra di dialogo conferma la creazione di una nuova brochure. Clic **[!UICONTROL Apri]** per aprire la brochure in modalità di modifica.

   <!--![chlimage_1-106](assets/.png) -->

   In alternativa, chiudere la finestra di dialogo e passare alla cartella nella pagina Modelli visualizzata per visualizzare la brochure creata. Il tipo di materiale promozionale viene visualizzato sulla miniatura nella vista a schede. Ad esempio, in questo caso, la parola [!UICONTROL Brochure] viene visualizzato sulla miniatura.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Modificare un materiale promozionale {#editing-a-collateral}

Potete modificare un materiale promozionale subito dopo averlo creato. In alternativa, è possibile aprirlo da [!UICONTROL Modelli] pagina della risorsa.

1. Per aprire il materiale promozionale per la modifica, effettuare una delle seguenti operazioni:

   * Aprire il materiale promozionale (in questo caso la brochure) creato nel passaggio 7 di [Creare un pezzo di materiale promozionale](/help/assets/asset-templates.md#creating-a-collateral).
   * Dalla pagina Modelli, individua la cartella in cui è stato creato il materiale promozionale, quindi fai clic su [!UICONTROL Modifica] azione rapida sulla miniatura di un elemento collaterale.
   * Nella pagina della risorsa del materiale promozionale, fai clic su **[!UICONTROL Modifica]** dalla barra degli strumenti.
   * Seleziona il materiale promozionale e fai clic su **[!UICONTROL Modifica]** dalla barra degli strumenti.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   Il Trova risorse e l’editor di testo sono visualizzati a sinistra della pagina. L’editor di testo è aperto per impostazione predefinita.

   Utilizza l’editor di testo per modificare il testo da visualizzare nel campo di testo. È possibile modificare la dimensione, lo stile, il colore e il tipo di carattere a livello di tag.

   Per utilizzare il Trova risorse, puoi sfogliare o cercare immagini in [!DNL Experience Manager Assets] e sostituisci le immagini modificabili nel modello con immagini di tua scelta.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Le immagini modificabili vengono visualizzate a destra. Per rendere modificabile un campo in [!DNL Experience Manager Assets], il campo corrispondente nel modello deve essere taggato in [!DNL InDesign]. In altre parole, devono essere contrassegnate come modificabili in [!DNL InDesign].

   >[!NOTE]
   >
   >Assicurati che il tuo [!DNL Experience Manager] l’implementazione è integrata con un [!DNL InDesign Server] per abilitare [!DNL Experience Manager Assets] per estrarre dati da [!DNL InDesign] e renderlo disponibile per la modifica. Per ulteriori informazioni, consulta [Integrare Experience Manager Assets con InDesign Server](/help/assets/indesign.md).

1. Per modificare il testo in un campo modificabile, fare clic sul campo di testo nell&#39;elenco dei campi modificabili e modificare il testo nel campo.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   È possibile modificare le proprietà del testo, ad esempio lo stile, il colore e le dimensioni del carattere, utilizzando le opzioni disponibili.

1. Seleziona **[!UICONTROL Anteprima]** per visualizzare in anteprima le modifiche apportate al testo.

1. Per scambiare un&#39;immagine, selezionare **[!UICONTROL Asset Finder]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. Seleziona il campo immagine dall’elenco dei campi modificabili, quindi trascina l’immagine desiderata dal selettore risorse al campo modificabile.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   Puoi anche cercare le immagini utilizzando parole chiave, tag e in base al loro stato di pubblicazione. È possibile sfogliare [!DNL Experience Manager Assets] e passare alla posizione dell&#39;immagine desiderata.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Seleziona **[!UICONTROL Anteprima]** in modo da poter visualizzare l&#39;anteprima dell&#39;immagine.
1. Per modificare una pagina specifica in un materiale promozionale composto da più pagine, utilizza il navigatore pagine in basso.

1. Seleziona **[!UICONTROL Anteprima]** sulla barra degli strumenti per visualizzare in anteprima tutte le modifiche. Seleziona **[!UICONTROL Fine]** per salvare le modifiche apportate al materiale promozionale.

   >[!NOTE]
   >
   >Le opzioni Anteprima e Fine sono attivate solo quando i campi dell’immagine modificabile all’interno del materiale promozionale non presentano icone mancanti. Se nel materiale promozionale sono presenti icone mancanti, è perché [!DNL Experience Manager] non è in grado di risolvere le immagini in [!DNL InDesign] modello. Di solito, [!DNL Experience Manager] non è in grado di risolvere le immagini nei seguenti casi:
   >
   >* Le immagini non sono incorporate nel sottostante [!DNL InDesign] modello.
   >* Le immagini sono collegate dal file system locale.
   >
   >Per abilitare [!DNL Experience Manager] per risolvere le immagini, effettuare le seguenti operazioni:
   >
   >* Incorpora immagini durante la creazione [!DNL InDesign] modelli (vedere [Informazioni su collegamenti e immagini incorporate](https://helpx.adobe.com/indesign/using/graphics-links.html)).
   >* Montaggio [!DNL Experience Manager] nel file system locale, quindi mappa le icone mancanti con le risorse esistenti in [!DNL Experience Manager].
   >
   >Per ulteriori informazioni sull&#39;utilizzo di [!DNL InDesign] documenti, vedi [best practice per l’utilizzo dei documenti InDesign in Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Per generare una rappresentazione PDF per la brochure, seleziona l’opzione Acrobat nella finestra di dialogo, quindi fai clic su **[!UICONTROL Continua]**.
1. Il materiale promozionale viene creato nella cartella con cui hai iniziato. Per visualizzare le rappresentazioni, apri il materiale promozionale e scegli **[!UICONTROL Rappresentazioni]** dall&#39;elenco GlobalNav.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Seleziona la copia trasformata PDF dall’elenco delle copie trasformate in modo da poter scaricare il file PDF. Apri il file PDF per rivedere il materiale promozionale.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Unisci materiale promozionale {#merge-collateral}

1. In [!DNL Experience Manager] interfaccia, seleziona [!UICONTROL Risorse] nella pagina Navigazione.

1. Dalle opzioni, seleziona **[!UICONTROL Modelli]**.

1. Seleziona **[!UICONTROL Crea]**, quindi dal menu, seleziona **[!UICONTROL Unisci]**.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. Dalla sezione [!UICONTROL Unione modelli] pagina, seleziona **[!UICONTROL Unisci]** ![aggiungere risorse](assets/do-not-localize/assets_add_icon.png).

1. Passare alla posizione del materiale promozionale che si desidera unire, selezionare le miniature del materiale promozionale che si desidera unire per selezionarle.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Puoi anche cercare i modelli dalla casella Omnisearch.

   È possibile sfogliare [!DNL Experience Manager Assets] nel repository o nelle raccolte, passare alla posizione dei modelli desiderati e selezionarli per l&#39;unione.

   Puoi applicare vari filtri per cercare i modelli desiderati. Ad esempio, puoi cercare modelli in base al tipo di file o ai tag.

1. Seleziona **[!UICONTROL Successivo]** dalla barra degli strumenti.
1. In **[!UICONTROL Anteprima e riordina]** , ridisporre i modelli se necessario e visualizzare in anteprima la selezione dei modelli da unire. Dalla barra degli strumenti, seleziona **[!UICONTROL Successivo]**.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. In [!UICONTROL Configura modello] , specificare un nome per il materiale promozionale. Facoltativamente, specifica i tag che ritieni appropriati. Se desideri esportare l’output in formato PDF, seleziona **[!UICONTROL Acrobat (.PDF)]**. Per impostazione predefinita, il materiale promozionale viene esportato in JPG e [!DNL InDesign] formato. Per modificare la miniatura di visualizzazione del materiale promozionale su più pagine, fai clic su **[!UICONTROL Cambia miniatura]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Seleziona **[!UICONTROL Salva]**, quindi chiudere la finestra di dialogo selezionando **[!UICONTROL OK]**. Il materiale promozionale di più pagine viene creato nella cartella che hai iniziato con.

   >[!NOTE]
   >
   >Non è possibile modificare un materiale promozionale unito in un secondo momento né utilizzarlo per creare un altro materiale promozionale.

## Best practice e limitazioni {#best-practices-limitations-tips}

* Il [!DNL InDesign] editor in [!DNL Experience Manager] funziona a livello di tag e tutto il testo sotto un singolo tag è considerato una singola entità. Per mantenere la formattazione e gli stili del testo durante la modifica, assegnare separatamente tag a ciascun paragrafo (o al testo con stili diversi).
