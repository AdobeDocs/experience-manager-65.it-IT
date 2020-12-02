---
title: Condizioni nelle comunicazioni interattive
seo-title: Condizioni nelle comunicazioni interattive
description: Creazione e modifica di frammenti di condizione da utilizzare nelle comunicazioni interattive. Questa condizione è uno dei quattro tipi di frammenti di documento utilizzati per creare comunicazioni interattive. Gli altri tre sono testi, elenchi e frammenti di layout.
seo-description: Creazione e modifica di condizioni da utilizzare nelle comunicazioni interattive
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 0%

---


# Condizioni nelle comunicazioni interattive{#conditions-in-interactive-communications}

Creazione e modifica di frammenti di condizione da utilizzare nelle comunicazioni interattive. Questa condizione è uno dei quattro tipi di frammenti di documento utilizzati per creare comunicazioni interattive. Gli altri tre sono testi, elenchi e frammenti di layout.

## Panoramica {#overview}

Condizione è un frammento di documento che è possibile includere in una comunicazione interattiva. Gli altri frammenti di documento sono [text](../../forms/using/texts-interactive-communications.md), un elenco e un frammento di layout. Le condizioni consentono di definire una o più risorse contestuali da includere in una comunicazione interattiva basata sui dati e sulle regole fornite.

Esempi:

* In un estratto conto della carta di credito, visualizzare l&#39;immagine della tariffa annuale e della carta di credito della carta di credito in base al tipo di carta di credito del cliente.
* In un promemoria di scadenza premio assicurativo, visualizzare i calcoli delle imposte in base alle imposte dello stato del cliente.

Le risorse nelle condizioni di cui viene eseguito il rendering in base alle regole applicate e ai valori passati alla regola. Le regole nelle condizioni possono controllare i valori nei seguenti tipi di dati:

* Proprietà del modello dati modulo associato
* Qualsiasi variabile creata nella condizione
* Stringhe
* Numeri
* Espressioni matematiche
* Date

## Crea condizione {#createcondition}

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.
1. Selezionare **[!UICONTROL Crea]** > **[!UICONTROL Condizione]**.
1. Specificate le seguenti informazioni:

   * **[!UICONTROL Titolo]**: (Facoltativo) Immettere il titolo per la condizione. I titoli non devono essere univoci e possono contenere caratteri speciali e caratteri non inglesi. Le condizioni sono indicate dai titoli (se disponibili), ad esempio nelle miniature e nelle proprietà.
   * **[!UICONTROL Nome]**: Nome univoco della condizione, all’interno di una cartella. In uno stato non possono esistere due frammenti di documento (testo, condizione o elenco) con lo stesso nome all’interno di una cartella. Nel campo Nome, è possibile immettere solo caratteri, numeri e trattini della lingua inglese. Il campo Nome viene compilato automaticamente in base al campo Titolo. I caratteri speciali, gli spazi, i numeri e i caratteri non inglesi immessi nel campo Titolo vengono sostituiti con i trattini nel campo Nome. Anche se il valore nel campo Titolo viene automaticamente copiato nel campo Nome, è possibile modificarlo.

   * **[!UICONTROL Descrizione]**: Digitare una descrizione del frammento di documento.
   * **[!UICONTROL Modello]** dati modulo: Facoltativamente, selezionare il pulsante di opzione Modello dati modulo per creare la condizione in base a un modello dati del modulo. Quando si seleziona il pulsante di scelta Modello dati modulo, viene visualizzato il campo **[!UICONTROL Modello dati modulo]**. Individuare e selezionare un modello dati del modulo. Durante la creazione di una condizione per una comunicazione interattiva, accertatevi di utilizzare lo stesso modello dati che intendete utilizzare nella comunicazione interattiva. Per ulteriori informazioni sul modello di dati del modulo, vedere [Integrazione dei dati](../../forms/using/data-integration.md).

   * **[!UICONTROL Tag]**: Se necessario, per creare un tag personalizzato immettete un valore nel campo di testo e toccate Invio. Quando salvate questa condizione, vengono creati i nuovi tag aggiunti.

1. Toccare **[!UICONTROL Next]**.

   Viene visualizzata la pagina Crea condizione.

   ![createcondizione](assets/createcondition.png)

1. Toccate **[!UICONTROL Aggiungi risorse]**.

   Selezionate la pagina Risorse e visualizzate il testo, gli elenchi, le condizioni e le immagini disponibili per l’aggiunta nella condizione.

   >[!NOTE]
   >
   >Nella pagina Seleziona risorse vengono visualizzate solo le risorse nuove e basate su FDM (create utilizzando lo stesso FDM della condizione creata).

1. Toccate le risorse appropriate per selezionarle da includere nella condizione, quindi toccate **[!UICONTROL Fine]**.

   Viene visualizzata la pagina Crea condizione in cui sono elencate le risorse aggiunte.

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   Per gestire le risorse in una condizione potete usare le seguenti opzioni:

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[Modifica ] di espulsione.** Toccate questa icona per rifiutare le modifiche eventualmente apportate alla risorsa e alla regola nella condizione.
   **[Modifica ] BAccept.** Toccate questa icona per accettare le modifiche apportate alla risorsa e alla regola nella condizione.
   **[Risorsa ] CDuplicate.** Toccate questa icona per creare una copia della risorsa insieme alla regola applicata, se presente, nella condizione. Quindi potete procedere alla modifica della regola e della risorsa per la risorsa duplicata. Duplicare una risorsa è utile per creare regole simili per visualizzare risorse alternative basate su un contesto particolare.
   **[Anteprima ] DShow.** Toccate questa icona per visualizzare un&#39;anteprima della risorsa nella pagina Crea\Modifica condizione.
   **&#39;server&#39; Reorder.** Toccate e tenete premuto questa icona per trascinare le risorse e riordinarle in una condizione.

   Potete selezionare le seguenti opzioni per specificare il comportamento della condizione in fase di esecuzione:

   * **Valutazione Di Più Risultati Disabilitata\Valutazione Di Più Risultati Abilitata**: Quando questa opzione è attivata (viene visualizzata come &quot;Valutazione di più risultati abilitata&quot;), vengono valutate tutte le regole e il risultato è la somma di tutte le regole vere. Se questa opzione è disabilitata (viene visualizzata come &quot;Valutazione di più risultati disabilitata&quot;), viene valutata solo la prima regola che si è rivelato vera e diventa l&#39;output della condizione.

   * **Interruzione** pagina: Selezionate questa opzione ( ![interruzione](assets/break.png)) per aggiungere un&#39;interruzione di pagina tra le risorse delle condizioni. Se questa opzione non è selezionata ( ![nobreak](assets/nobreak.png)), se una condizione è in eccesso alla pagina successiva nell&#39;output di stampa, l&#39;intera condizione viene spostata nella pagina successiva invece di interrompere la pagina tra le risorse nella condizione.

1. Toccate **[!UICONTROL Crea regola]** per aggiungere regole per visualizzare o nascondere le risorse, a seconda delle necessità. Per utilizzare le variabili nelle regole, vedere [creazione di variabili](#variables). Per ulteriori informazioni, vedere [Aggiunta di regole alla condizione](#ruleeditor).

   Le regole create vengono visualizzate nella colonna REGOLA nella schermata Crea condizione.

   ![createconditionscreenrulesaggiunto](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >È possibile inserire risorse nella condizione in cui sono già applicate delle regole o che si ripetono le operazioni.

1. Toccate **[!UICONTROL Salva]**.

   La condizione viene creata. Ora potete utilizzare la condizione come componente di base durante la creazione di una comunicazione interattiva.

   >[!NOTE]
   >
   >Per salvare una condizione nuova o modificata, è necessario disporre di almeno una regola per ciascuna risorsa aggiunta nella condizione.

## Modificare una condizione {#edit-a-condition}

È possibile modificare una condizione seguendo la procedura seguente. È inoltre possibile scegliere di modificare una condizione all&#39;interno di una comunicazione interattiva selezionando Modifica frammento nel menu a comparsa.

1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.
1. Passate alla condizione e selezionatela.
1. Toccate **[!UICONTROL Modifica]**.
1. Apportate le modifiche necessarie alla condizione. Per ulteriori informazioni sulle informazioni che è possibile modificare in una condizione, vedere [Crea condizione](#createcondition).
1. Toccate **[!UICONTROL Save]**, quindi toccate **[!UICONTROL Close]**.

## Creare le regole nella condizione {#ruleeditor}

Utilizzando l&#39;editor di regole in una condizione, potete creare regole per visualizzare o nascondere le risorse in base alle **condizioni preimpostate**. Queste condizioni possono essere costruite sulla base di:

* Stringhe
* Numeri
* Espressioni matematiche
* Date
* Proprietà del modello dati del modulo associato
* Qualsiasi [variabile](#variables) eventualmente creata

### Crea regola nella condizione {#create-rule-in-condition}

1. Durante la creazione o la modifica di una condizione, toccate l&#39;icona ![ruleeditoricon](assets/ruleeditoricon.png) (Editor regole) per la risorsa pertinente.

   Viene visualizzata la finestra di dialogo Crea regola. Oltre a stringa, numero, espressione matematica e data, nell&#39;Editor regola sono disponibili anche le seguenti informazioni per la creazione di istruzioni delle regole:

   * Proprietà del modello dati del modulo associato
   * Qualsiasi [variabile](#variables) eventualmente creata.

   ![createruledialog](assets/createruledialog.png)

   Selezionare l&#39;opzione appropriata da valutare.

   >[!NOTE]
   >
   >La proprietà Collection non è supportata per la creazione di regole per la visualizzazione delle risorse.

1. Selezionare l&#39;operatore appropriato per valutare la regola, ad esempio È uguale a, Contiene e Inizia con.
1. Inserire l&#39;espressione di valutazione, la stringa, la proprietà del modello dati, la variabile o la data.

   ![Regola per visualizzare una risorsa quando il tipo di criterio è standard](assets/ruleincondition.png)

   Regola per visualizzare una risorsa quando il tipo di criterio è standard

   * Durante la creazione o la modifica di una regola, potete anche toccare ![icon_resize](assets/icon_resize.png) (Ridimensiona) per espandere la finestra di dialogo Crea regola/Modifica regola. La finestra di dialogo estesa a finestra intera consente di creare [variabili](#variables) per creare regole. Toccate di nuovo Ridimensiona per tornare alla finestra di dialogo Crea regola.

   * È inoltre possibile creare più condizioni in una regola.

1. Toccate **[!UICONTROL Chiudi]**.

   La regola viene applicata alla risorsa.

## Creazione e utilizzo di variabili in una condizione {#variables}

Durante la creazione o la modifica di una regola in una condizione, potete toccare ![icon_resize](assets/icon_resize.png) (Ridimensiona) per espandere la finestra di dialogo Crea regola\Modifica regola. La finestra di dialogo estesa e completa consente di:

* Creazione e utilizzo di variabili nella regola
* Trascinare le proprietà e le variabili del modello dati modulo nella regola

Toccate nuovamente Ridimensiona per tornare alla finestra di dialogo Crea regola\Modifica regola.

### Creare variabili {#create-variables}

1. Durante la creazione o la modifica di una regola in una condizione, potete toccare ![icon_resize](assets/icon_resize.png) (Ridimensiona) per espandere la finestra di dialogo Crea regola\Modifica regola.

   Viene visualizzata la finestra di dialogo Espansa e completa.

   ![expandeditrulefinestra di dialogo](assets/expandededitruledialog.png)

1. Nel riquadro a sinistra, toccare **[!UICONTROL Variabili]**.

   Viene visualizzato il riquadro Variabili.

   ![espandeditrighvariabili](assets/expandededitrulevariables.png)

1. Toccate **[!UICONTROL Crea]**.

   Viene visualizzato il riquadro Crea variabili.

1. Immettere le informazioni seguenti e toccare **[!UICONTROL Crea]**:

   * **[!UICONTROL Nome]**: Nome della variabile.
   * **[!UICONTROL Descrizione]**: Facoltativamente, immettete una descrizione della variabile.
   * **[!UICONTROL Tipo]**: Selezionare un tipo di variabile: Stringa, Numero, Booleano o Data.
   * **[!UICONTROL Consenti solo]** valori specifici: Per le variabili String e Number, potete fare in modo che l&#39;agente scelga da un set specifico di valori per un segnaposto nell&#39;interfaccia utente dell&#39;agente. Per specificare il set di valori, selezionare questa opzione e specificare i valori separati da virgola consentiti nel campo **[!UICONTROL Values]**.

1. Toccate **[!UICONTROL Crea]**.

   La variabile viene creata ed elencata nel riquadro Variabili.

1. Per inserire una variabile nella regola, trascinatela in un segnaposto per un&#39;opzione nella regola.
1. Dopo aver creato una regola valida, toccare **[!UICONTROL Fine]**.

   Se necessario, apportate ulteriori modifiche alla condizione e salvatela.

