---
title: Condizioni delle comunicazioni interattive
seo-title: Conditions in Interactive Communications
description: 'Creazione e modifica di frammenti di condizione da utilizzare nelle comunicazioni interattive: condizione è uno dei quattro tipi di frammenti di documento utilizzati per la creazione di comunicazioni interattive. Gli altri tre sono testi, elenchi e frammenti di layout.'
seo-description: Creating and editing conditions to be used in Interactive Communications
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
feature: Interactive Communication
exl-id: 0c0dc6a2-b889-4516-8e08-1e9d31be2cce
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# Condizioni delle comunicazioni interattive{#conditions-in-interactive-communications}

Creazione e modifica di frammenti di condizione da utilizzare nelle comunicazioni interattive: condizione è uno dei quattro tipi di frammenti di documento utilizzati per la creazione di comunicazioni interattive. Gli altri tre sono testi, elenchi e frammenti di layout.

## Panoramica {#overview}

Condizione è un frammento di documento che è possibile includere in una comunicazione interattiva. Gli altri frammenti di documento sono [text](../../forms/using/texts-interactive-communications.md), elenco e frammento di layout. Le condizioni ti consentono di definire una o più risorse contestuali da includere in una comunicazione interattiva basata sui dati e sulle regole forniti.

Esempi:

* In un estratto conto della carta di credito, visualizzare l&#39;immagine della commissione annuale della carta di credito e della carta di credito in base al tipo di carta di credito del cliente.
* In un sollecito di premio assicurativo, visualizzare i calcoli di imposta in base alle imposte dello stato del cliente.

Le risorse nelle condizioni di cui viene eseguito il rendering in base alle regole applicate e ai valori passati alla regola. Le regole nelle condizioni possono controllare i valori nei seguenti tipi di dati:

* Proprietà del modello dati modulo associato
* Qualsiasi variabile creata nella condizione
* Stringhe
* Numeri
* Espressioni matematiche
* Date

## Crea condizione {#createcondition}

1. Seleziona **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.
1. Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Condizione]**.
1. Specifica le seguenti informazioni:

   * **[!UICONTROL Titolo]**: (Facoltativo) Immetti il titolo della condizione. I titoli non devono essere univoci e possono contenere caratteri speciali e caratteri non inglesi. Le condizioni sono indicate dai loro titoli (se disponibili), ad esempio nelle miniature e nelle proprietà.
   * **[!UICONTROL Nome]**: Nome univoco della condizione all’interno di una cartella. In uno stato non possono esistere due frammenti di documento (testo, condizione o elenco) con lo stesso nome all’interno di una cartella. Nel campo Nome è possibile immettere solo caratteri, numeri e trattini della lingua inglese. Il campo Nome viene compilato automaticamente in base al campo Titolo . I caratteri speciali, gli spazi, i numeri e i caratteri non inglesi immessi nel campo Titolo vengono sostituiti dai trattini nel campo Nome . Anche se il valore nel campo Titolo viene copiato automaticamente nel campo Nome, è possibile modificarlo.

   * **[!UICONTROL Descrizione]**: Digitare una descrizione del frammento di documento.
   * **[!UICONTROL Modello dati modulo]**: Facoltativamente, selezionare il pulsante di opzione Modello dati modulo per creare la condizione in base a un modello dati modulo. Quando si seleziona il pulsante di opzione Modello dati modulo , **[!UICONTROL Modello dati modulo]** viene visualizzato il campo . Sfogliare e selezionare un modello dati del modulo. Durante la creazione di una condizione per una comunicazione interattiva, assicurati di utilizzare lo stesso modello dati che intendi utilizzare nella comunicazione interattiva. Per ulteriori informazioni sul modello dati modulo, vedere [Integrazione dei dati](../../forms/using/data-integration.md).

   * **[!UICONTROL Tag]**: Facoltativamente, per creare un tag personalizzato inserisci il valore nel campo di testo e tocca Invio. Quando salvi questa condizione, vengono creati i nuovi tag aggiunti.

1. Tocca **[!UICONTROL Successivo]**.

   Viene visualizzata la pagina Crea condizione .

   ![createcondizione](assets/createcondition.png)

1. Tocca **[!UICONTROL Aggiungere risorse]**.

   Seleziona la pagina Risorse viene visualizzata e visualizza i testi, gli elenchi, le condizioni e le immagini disponibili per l’aggiunta nella condizione.

   >[!NOTE]
   >
   >Nella pagina Seleziona risorse vengono visualizzate solo le risorse nuove e prive di base e le risorse basate su FDM (create utilizzando lo stesso FDM della condizione che si sta creando).

1. Tocca le risorse appropriate per selezionarle da includere nella condizione, quindi tocca **[!UICONTROL Fine]**.

   Viene visualizzata la pagina Crea condizione , in cui sono elencate le risorse aggiunte.

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   Per gestire le risorse in una condizione, puoi utilizzare le seguenti opzioni:

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[A] Rifiuta modifica.** Tocca questa icona per rifiutare le modifiche eventualmente apportate alla risorsa e alla regola nella condizione .
   **[B] Accetta Modifica.** Tocca questa icona per accettare le modifiche apportate alla risorsa e alla regola nella condizione .
   **[C] Duplica risorsa.** Tocca questa icona per creare una copia della risorsa insieme alla regola applicata, se presente, nella condizione . Quindi puoi procedere alla modifica della regola e della risorsa per la risorsa duplicata. La duplicazione di una risorsa è utile per creare regole simili per visualizzare risorse alternative in base a un particolare contesto.
   **[D] Mostra anteprima.** Tocca questa icona per visualizzare un’anteprima della risorsa nella pagina Crea\Modifica condizione .
   **Riordino &#39;server&#39;.** Tocca e tieni premuto questa icona per trascinare le risorse e riordinarle in una condizione.

   Puoi selezionare le seguenti opzioni per specificare il comportamento della condizione in fase di runtime:

   * **Valutazione di più risultati disattivata\Valutazione di più risultati abilitata**: Quando questa opzione è abilitata (viene visualizzata come &quot;Valutazione di più risultati abilitata&quot;), vengono valutate tutte le regole e il risultato è la somma di tutte le regole vere. Se questa opzione è disabilitata (viene visualizzata come &quot;Valutazione di più risultati disabilitata&quot;), viene valutata solo la prima regola che risulta vera e diventa l’output della condizione.

   * **Interruzione di pagina**: Seleziona questa opzione ( ![break](assets/break.png)) per aggiungere un’interruzione di pagina tra le risorse delle condizioni. Quando questa opzione non è selezionata ( ![rumore](assets/nobreak.png)), se una condizione si estende alla pagina successiva nell’output di stampa, l’intera condizione viene spostata nella pagina successiva anziché essere suddivisa nella pagina tra le risorse nella condizione .

1. Tocca **[!UICONTROL Crea regola]** per aggiungere regole per visualizzare o nascondere le risorse, a seconda delle necessità. Per utilizzare le variabili nelle regole, vedi [creazione di variabili](#variables). Per ulteriori informazioni, consulta [Aggiunta di regole alla condizione](#ruleeditor).

   Le regole create vengono visualizzate nella colonna REGOLA nella schermata Crea condizione .

   ![createconditionscreenrulesaggiunta](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >È possibile inserire risorse nella condizione in cui sono già applicate regole o ripeterle.

1. Tocca **[!UICONTROL Salva]**.

   La condizione viene creata. È ora possibile utilizzare la condizione come blocco predefinito durante la creazione di una comunicazione interattiva.

   >[!NOTE]
   >
   >Per salvare una condizione nuova o modificata, è necessario disporre di almeno una regola per ciascuna risorsa aggiunta nella condizione.

## Modificare una condizione {#edit-a-condition}

Puoi modificare una condizione seguendo questi passaggi. È inoltre possibile scegliere di modificare una condizione all’interno di una comunicazione interattiva selezionando Modifica frammento nel menu a comparsa.

1. Seleziona **[!UICONTROL Forms]** > **[!UICONTROL Frammenti documento]**.
1. Passa alla condizione e selezionala.
1. Tocca **[!UICONTROL Modifica]**.
1. Apporta le modifiche necessarie alla condizione . Per ulteriori dettagli sulle informazioni che è possibile modificare in una condizione, consulta [Crea condizione](#createcondition).
1. Tocca **[!UICONTROL Salva]** quindi tocca **[!UICONTROL Chiudi]**.

## Creare regole in condizioni {#ruleeditor}

Utilizzando l’editor di regole in una condizione, puoi creare regole per visualizzare o nascondere le risorse in base a **condizioni predefinite**. Queste condizioni possono essere costruite in base a:

* Stringhe
* Numeri
* Espressioni matematiche
* Date
* Proprietà del modello dati del modulo associato
* Qualsiasi [variables](#variables) che hai creato

### Crea regola in condizioni {#create-rule-in-condition}

1. Durante la creazione o la modifica di una condizione, tocca ![ruleeditoricon](assets/ruleeditoricon.png) (Editor regole) icona per la risorsa pertinente.

   Viene visualizzata la finestra di dialogo Crea regola. Oltre a stringa, numero, espressione matematica e data, nell’Editor regole sono disponibili anche le seguenti istruzioni per la creazione di istruzioni delle regole:

   * Proprietà del modello dati del modulo associato
   * Qualsiasi [variables](#variables) che potresti aver creato.

   ![dialogo createrolino](assets/createruledialog.png)

   Selezionare l’opzione appropriata da valutare.

   >[!NOTE]
   >
   >La proprietà Collection non è supportata per la creazione di regole per la visualizzazione delle risorse.

1. Seleziona l’operatore appropriato per valutare la regola, ad esempio È uguale a, Contiene e Inizia con.
1. Inserire l&#39;espressione di valutazione, la stringa, la proprietà del modello dati, la variabile o la data.

   ![Regola per mostrare una risorsa quando il tipo di criterio è standard](assets/ruleincondition.png)

   Regola per mostrare una risorsa quando il tipo di criterio è standard

   * Durante la creazione o la modifica di una regola, puoi anche toccare ![icon_resize](assets/icon_resize.png) (Ridimensiona) per espandere la finestra di dialogo Crea regola/Modifica regola. La finestra di dialogo espansa e completa consente di creare [variables](#variables) per creare regole. Tocca nuovamente Ridimensiona per tornare alla finestra di dialogo regolare Crea regola .

   * Puoi anche creare più condizioni in una regola.

1. Toccate **[!UICONTROL Chiudi]**.

   La regola viene applicata alla risorsa.

## Creazione e utilizzo di variabili in una condizione {#variables}

Durante la creazione o la modifica di una regola in una condizione, puoi toccare ![icon_resize](assets/icon_resize.png) (Ridimensiona) per espandere la finestra di dialogo Crea regola\Modifica regola. La finestra di dialogo espansa a finestra intera consente di:

* Creare e utilizzare le variabili nella regola
* Proprietà e variabili del modello dati del modulo trascinate nella regola

Toccare nuovamente Ridimensiona per tornare alla finestra di dialogo Crea regola\Modifica regola.

### Creare variabili {#create-variables}

1. Durante la creazione o la modifica di una regola in una condizione, puoi toccare ![icon_resize](assets/icon_resize.png) (Ridimensiona) per espandere la finestra di dialogo Crea regola\Modifica regola.

   Viene visualizzata la finestra di dialogo Espansa a finestra intera.

   ![expandeditrulefinestra di dialogo](assets/expandededitruledialog.png)

1. Nel riquadro a sinistra, tocca **[!UICONTROL Variabili]**.

   Viene visualizzato il riquadro Variabili.

   ![variabili expandeditrighables](assets/expandededitrulevariables.png)

1. Tocca **[!UICONTROL Crea]**.

   Viene visualizzato il riquadro Crea variabili .

1. Immetti le seguenti informazioni e tocca **[!UICONTROL Crea]**:

   * **[!UICONTROL Nome]**: Nome della variabile.
   * **[!UICONTROL Descrizione]**: Facoltativamente, inserisci una descrizione della variabile.
   * **[!UICONTROL Tipo]**: Seleziona un tipo di variabile: Stringa, Numero, Booleano o Data.
   * **[!UICONTROL Consenti solo valori specifici]**: Per le variabili String e Number, è possibile assicurarsi che l&#39;agente scelga da un set specifico di valori per un segnaposto nell&#39;interfaccia utente dell&#39;agente. Per specificare il set di valori, seleziona questa opzione e specifica i valori separati da virgole consentiti nel **[!UICONTROL Valori]** campo .

1. Tocca **[!UICONTROL Crea]**.

   La variabile viene creata ed elencata nel riquadro Variabili .

1. Per inserire una variabile nella regola, trascina e rilascia la variabile in un segnaposto per un’opzione nella regola.
1. Dopo aver costruito una regola valida, tocca **[!UICONTROL Fine]**.

   Procedi a apportare ulteriori modifiche, se necessario, nella condizione e salvarla.
