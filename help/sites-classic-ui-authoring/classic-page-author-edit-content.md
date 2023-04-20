---
title: Modifica del contenuto di una pagina
description: Il contenuto viene aggiunto utilizzando componenti che possono essere trascinati sulla pagina. che possono quindi essere modificati, spostati o eliminati.
uuid: e7b65ceb-263c-46f2-91e3-11dec3a016fa
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: de321869-ebf9-41a1-8203-e12bdb088678
docset: aem65
exl-id: e1b5aea0-983c-4e7b-9d35-d7beeee45dc7
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 13%

---

# Modifica del contenuto di una pagina{#editing-page-content}

Una volta creata la pagina (nuova o come parte di un lancio o di una Live Copy) è possibile modificare il contenuto per apportare gli aggiornamenti necessari.

Il contenuto viene aggiunto utilizzando [componenti](/help/sites-classic-ui-authoring/classic-page-author-default-components.md) (in base al tipo di contenuto) trascinabile sulla pagina. che possono quindi essere modificati, spostati o eliminati.

>[!NOTE]
>
>Il tuo account deve [diritti di accesso appropriati](/help/sites-administering/security.md) e [permissions](/help/sites-administering/security.md#permissions) per modificare le pagine; ad esempio, aggiungere, modificare o eliminare componenti, aggiungere annotazioni, sbloccare.
>
>Nell’eventualità di problemi, rivolgiti al tuo amministratore di sistema.

## Barra laterale {#sidekick}

La barra laterale è uno strumento chiave per la creazione delle pagine. Si tratta di un elemento mobile durante l’authoring di una pagina, che diventa sempre visibile.

Sono disponibili diverse schede e icone, tra cui:

* Componenti
* Pagina
* Informazioni
* Controllo delle versioni
* Flusso di lavoro
* Modalità
* Scaffolding
* ClientContext
* Siti Web

![chlimage_1-71](assets/chlimage_1-71.png)

Queste consentono di accedere a un&#39;ampia gamma di funzionalità; compresi:

* [selezione dei componenti](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [visualizzazione dei riferimenti](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [accesso al registro di controllo](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [modalità di commutazione](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* [creazione](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version), [ripristino](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick) e [confronto](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version) versioni

* [pubblicazione](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page), [annullamento della pubblicazione](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page) una pagina

* [modifica delle proprietà di pagina](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [impalcatura](/help/sites-authoring/scaffolding.md)

* [contesto client](/help/sites-administering/client-context.md)

## Inserimento di un componente {#inserting-a-component}

### Inserimento di un componente {#inserting-a-component-1}

Dopo aver aperto la pagina, puoi iniziare ad aggiungere il contenuto. A tale scopo, è necessario aggiungere i componenti (o paragrafi).

Per inserire un nuovo componente:

1. Esistono diversi metodi per selezionare il tipo di paragrafo da inserire:

   * Fare doppio clic sull’area etichettata **Trascina qui i componenti o le risorse .** - il **Inserisci nuovo componente** viene visualizzata la barra degli strumenti. Seleziona un componente e fai clic su **OK**.

   * Trascinate un componente dalla barra degli strumenti mobile (o barra laterale) per inserire un nuovo paragrafo.
   * Fai clic con il pulsante destro del mouse su un paragrafo esistente e seleziona **Nuovo...** - Viene visualizzata la barra degli strumenti Inserisci nuovo componente . Seleziona un componente e fai clic su **OK**.

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. Sia nella barra laterale che nella **Inserisci nuovo componente** viene visualizzato un elenco dei componenti disponibili (tipi di paragrafo). Questi possono essere suddivisi in varie sezioni (ad esempio Generale, Colonne, ecc.), che possono essere espanse come necessario.

   A seconda dell’ambiente di produzione, queste scelte possono variare. Per informazioni complete sui componenti, consulta [Componenti predefiniti](/help/sites-classic-ui-authoring/classic-page-author-default-components.md).

1. Inserisci il componente desiderato nella pagina. Quindi fai doppio clic sul paragrafo; viene visualizzata una finestra che consente di configurare il paragrafo e aggiungere contenuto.

### Inserimento di un componente utilizzando Content Finder {#inserting-a-component-using-the-content-finder}

Puoi anche aggiungere un nuovo componente alla pagina trascinando una risorsa dalla sezione [Content Finder](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder). In questo modo verrà creato automaticamente un nuovo componente del tipo appropriato contenente la risorsa.

Questo vale per i seguenti tipi di risorse (alcune dipenderanno dal sistema di pagine/paragrafi):

| Tipo risorsa | Tipo componente risultante |
|---|---|
| Immagine | Immagine |
| Documento | Scarica |
| Prodotto | Prodotto |
| Video | Flash |

>[!NOTE]
>
>Puoi configurare questo comportamento per l’installazione in uso. Vedi [La configurazione di un sistema di paragrafi in modo che il trascinamento di una risorsa crei un’istanza di componente](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) per ulteriori dettagli.

Per creare un componente trascinando uno dei tipi di risorsa indicati sopra:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
1. Apri [Content Finder](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder).
1. Trascina la risorsa desiderata nella posizione desiderata. La [segnaposto componente](#componentplaceholder) mostra dove sarà posizionato il componente.

   Un componente, appropriato per il tipo di risorsa, verrà creato nella posizione desiderata, che conterrà la risorsa selezionata.

1. [Modifica](#editmovecopypastedelete) il componente, se necessario.

## Modifica di un componente (contenuto e proprietà) {#editing-a-component-content-and-properties}

Per modificare un paragrafo esistente, effettuare una delle seguenti operazioni:

* **Fare doppio clic** paragrafo per aprirlo. Viene visualizzata la stessa finestra visualizzata quando è stato creato il paragrafo con il contenuto esistente. Apporta le modifiche desiderate e fai clic su **OK**.

* **Fai clic con il pulsante destro del mouse** il paragrafo e fai clic su **Modifica**.

* **Fai clic su** due volte sul paragrafo (doppio clic lento) per passare alla modalità di modifica diretta. È possibile modificare direttamente il testo sulla pagina, anziché all’interno di una finestra di dialogo. In questa modalità, nella parte superiore della pagina sarà disponibile una barra degli strumenti. È sufficiente apportare le modifiche e verranno salvate automaticamente.

## Spostamento di un componente {#moving-a-component}

Per spostare un paragrafo:

>[!NOTE]
>
>Per spostare un componente puoi anche utilizzare [Taglia e Incolla](#cut-copy-paste-a-component).

1. Selezionate il paragrafo da spostare:

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. Trascina il paragrafo nella nuova posizione. AEM indica dove è possibile spostare il paragrafo con un segno di spunta verde. Rilascia nella posizione desiderata.
1. Il paragrafo è stato spostato:

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## Eliminazione di un componente {#deleting-a-component}

Per eliminare un paragrafo:

1. Seleziona il paragrafo e **fare clic con il pulsante destro del mouse**:

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. Seleziona **Elimina** dal menu. AEM WCM richiede la conferma dell’eliminazione del paragrafo, poiché questa azione non può essere annullata.
1. Fai clic su **OK**.

>[!NOTE]
>
>Se hai impostato [Proprietà utente per visualizzare la barra degli strumenti di modifica globale](/help/sites-classic-ui-authoring/author-env-user-props.md) è inoltre possibile eseguire determinate azioni sui paragrafi utilizzando la **Copia**, **Taglia**, **Incolla**, **Elimina** pulsanti disponibili.
>
>Varie [scelte rapide da tastiera](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) sono anche disponibili.

## Operazioni di Taglia, Copia, Incolla su un componente {#cut-copy-paste-a-component}

Come quando [Eliminazione di un componente](#deleting-a-component) è possibile utilizzare il menu di scelta rapida per copiare, tagliare e/o incollare un componente

>[!NOTE]
>
>Se hai impostato [Proprietà utente per visualizzare la barra degli strumenti di modifica globale](/help/sites-classic-ui-authoring/author-env-user-props.md) è inoltre possibile eseguire determinate azioni sui paragrafi utilizzando la **Copia**, **Taglia**, **Incolla**, **Elimina** pulsanti disponibili.
>
>Varie [scelte rapide da tastiera](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) sono anche disponibili.

>[!NOTE]
>
>Le operazioni di taglio, copia e incolla dei contenuti sono supportate solo all’interno della stessa pagina.

## Componenti ereditati {#inherited-components}

I componenti ereditati possono essere il risultato di vari scenari, tra cui:

* [Gestione multisito](/help/sites-administering/msm.md); anche in combinazione con [impalcatura](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance).

* [Lanci](/help/sites-classic-ui-authoring/classic-launches.md) (se basato su Live Copy).
* Componenti specifici; ad esempio il sistema paragrafo ereditato in Geometrixx.

È possibile annullare l’ereditarietà, quindi riabilitarla. A seconda del componente, questo può essere disponibile da:

1. **Live Copy**

   Se un componente fa parte di una Live Copy o di un lancio, è indicato da un’icona a forma di lucchetto. Puoi fare clic sul lucchetto per annullare l’ereditarietà.

   * L’icona lucchetto viene visualizzata quando il componente è selezionato; ad esempio:

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * Il lucchetto viene inoltre visualizzato nella finestra di dialogo dei componenti; ad esempio:

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **Un Sistema Paragrafo Ereditato**

   Finestra di dialogo di configurazione. Ad esempio, come per il sistema paragrafo ereditato in Geometrixx:

   ![chlimage_1-74](assets/chlimage_1-74.png)

## Aggiunta di annotazioni {#adding-annotations}

[Annotazioni](/help/sites-classic-ui-authoring/classic-page-author-annotations.md) consentire ad altri autori di fornire feedback sui contenuti. Questo viene spesso utilizzato a scopo di revisione e convalida.

## Anteprima delle pagine   {#previewing-pages}

Sul bordo inferiore della barra laterale sono disponibili due icone importanti per l’anteprima delle pagine:

![](do-not-localize/chlimage_1-5.png)

* L’icona a forma di matita indica che è attiva la modalità di modifica, che consente di aggiungere, modificare, spostare o eliminare contenuti.

   ![](do-not-localize/chlimage_1-6.png)

* L’icona della lente di ingrandimento consente di selezionare la modalità di anteprima in cui la pagina viene visualizzata così come verrà visualizzata nell’ambiente di pubblicazione (a volte è necessario un aggiornamento della pagina):

   ![](do-not-localize/chlimage_1-7.png)

   In modalità anteprima la barra laterale viene ridotta. Fai clic sull’icona della freccia giù per tornare alla modalità di modifica:

   ![](do-not-localize/chlimage_1-8.png)

## Trova e sostituisci {#find-replace}

Per modifiche su larga scala della stessa frase a **[Trova e sostituisci](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)** l’opzione di menu consente di cercare e sostituire più istanze di una stringa all’interno di una sezione del sito web.

## Blocco di una pagina   {#locking-a-page}

AEM consente di bloccare una pagina in modo che nessun altro possa modificarne il contenuto. Questa funzione è utile quando apporti numerose modifiche a una pagina oppure quando devi bloccarla per un breve periodo di tempo.

>[!CAUTION]
>
>Il blocco di una pagina deve essere utilizzato con attenzione in quanto l’unica persona che può sbloccare una pagina è la persona che l’ha bloccata (o un account con privilegi di amministratore).

Per bloccare una pagina:

1. In **Siti Web** selezionare la pagina da bloccare.
1. Fai doppio clic sulla pagina per aprirla in modalità di modifica.
1. In **Pagina** scheda della barra laterale, seleziona **Blocca pagina**:

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   Un messaggio indica che la pagina è bloccata per altri utenti. Inoltre, nel riquadro a destra del **Siti Web** in AEM WCM la pagina viene visualizzata come bloccata ed è indicato l’utente che ha applicato il blocco.

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## Sblocco di una pagina {#unlocking-a-page}

Per sbloccare una pagina:

1. In **Siti Web** , seleziona la pagina da sbloccare.
1. Fai doppio clic sulla pagina per aprirla.
1. In **Pagina** scheda della barra laterale, seleziona **Sblocca pagina**.

## Annullamento e ripristino di operazioni di modifica delle pagine {#undoing-and-redoing-page-edits}

Quando la cornice contenuto della pagina è attiva, utilizza le seguenti scelte rapide da tastiera:

* Annulla: Ctrl+Z (Windows) o Comando+Z (Mac)
* Ripristina: Ctrl+Y (Windows) o Comando+Y (Mac)

Quando si annullano o si ripristinano operazioni di rimozione, aggiunta o spostamento di uno o più paragrafi, i paragrafi interessati sono indicati da un’evidenziazione intermittente (impostazione predefinita).

>[!NOTE]
>
>Per informazioni sulle possibilità di annullare e ripristinare le modifiche apportate a una pagina, consulta [Annullamento e ripristino di operazioni di modifica delle pagine - La teoria](#undoing-and-redoing-page-edits-the-theory).

## Annullamento e ripristino di operazioni di modifica delle pagine - La teoria {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>L&#39;amministratore di sistema può [configurare vari aspetti delle funzioni Annulla/Ripristina](/help/sites-administering/config-undo.md) in base ai requisiti della tua istanza.

AEM memorizza la cronologia delle azioni eseguite e la sequenza di esecuzione. È quindi possibile annullare diverse azioni nell’ordine in cui sono state eseguite. Quindi, puoi utilizzare Ripristina per riapplicare una o più azioni.

Se è selezionato un elemento nella pagina del contenuto, il comando Annulla e Ripristina si applica all’elemento selezionato, ad esempio un componente di testo.

Il comportamento dei comandi Annulla e Ripristina è simile a quello di altri programmi software. Utilizzare i comandi per ripristinare lo stato recente della pagina web mentre si prendono decisioni sul contenuto. Se ad esempio si sposta un paragrafo di testo altrove nella pagina, è possibile ricorrere al comando Annulla per riportarlo nella posizione originale. Se poi si decide di spostare nuovamente il paragrafo, utilizzare il comando Ripristina.

>[!NOTE]
>
>Operazioni disponibili:
>
>* Le azioni annullate possono essere ripristinate solo se dopo l’annullamento non sono state apportate altre modifiche alla pagina.
>* annullare un massimo di 20 azioni di modifica (impostazione predefinita).
>* anche utilizzare [Scelte rapide da tastiera](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) per annullare e ripristinare.
>


I comandi Annulla e Ripristina possono essere utilizzati per i seguenti tipi di modifiche alla pagina:

* Aggiunta, modifica, rimozione e spostamento di paragrafi
* Modifica diretta del contenuto del paragrafo
* Copiare, tagliare e incollare elementi all’interno di una pagina
* Copiare, tagliare e incollare elementi tra pagine diverse
* Aggiunta, rimozione e modifica di file e immagini
* Aggiunta, rimozione e modifica di annotazioni e schizzi
* Modifiche alla pagina di scaffolding
* Aggiunta e rimozione di riferimenti
* Modifica dei valori delle proprietà nelle finestre di dialogo dei componenti.

Per i campi modulo di cui viene eseguito il rendering dei componenti modulo non deve essere specificato alcun valore durante l’authoring delle pagine. Pertanto, i comandi Annulla e Ripristina non influiscono sulle modifiche apportate ai valori di questi tipi di componenti. Ad esempio, non è possibile annullare la selezione di un valore in un elenco a discesa.

>[!NOTE]
>
>Per annullare e ripristinare le modifiche apportate a file e immagini sono necessarie autorizzazioni speciali. Inoltre, la cronologia di annullamento per le modifiche a file e immagini ha una durata minima di ore. Oltre tale limite, la possibilità di annullare le modifiche non è garantita. L’amministratore può concedere le autorizzazioni e modificare l’intervallo predefinito di dieci ore.
