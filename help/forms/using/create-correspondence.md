---
title: Crea corrispondenza
seo-title: Crea corrispondenza
description: Dopo aver creato un modello di lettera, è possibile utilizzarlo per creare la corrispondenza in  AEM Forms gestendo dati, contenuto e allegati.
seo-description: Dopo aver creato un modello di lettera, è possibile utilizzarlo per creare la corrispondenza in  AEM Forms gestendo dati, contenuto e allegati.
uuid: 48cf2b26-c9b4-4127-9ea0-1b36addbff60
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 87742cb2-357b-421f-b79d-e355887ddec0
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '3720'
ht-degree: 0%

---


# Crea corrispondenza{#create-correspondence}

## Creare corrispondenza nell’interfaccia utente Crea corrispondenza {#create-correspondence-in-the-create-correspondence-user-interface}

Dopo la creazione di un modello di [lettera in Gestione](../../forms/using/create-letter.md)corrispondenza, l&#39;utente finale/agente/regolatore di credito può aprire la lettera nell&#39;interfaccia utente Crea corrispondenza e creare una corrispondenza immettendo i dati, configurando il contenuto e gestendo gli allegati. Infine, l&#39;agente o il regolatore delle attestazioni può gestire il contenuto in modalità di anteprima e inviare la lettera.

### Anteprima di una corrispondenza {#preview-a-correspondence}

Selezionate la lettera da visualizzare in anteprima con la procedura seguente:

1. Nella pagina Lettere, toccate **Seleziona**.
1. Selezionare la lettera appropriata toccandola.

   ![Seleziona lettera](assets/1_selectletter.png)

   Seleziona lettera

1. Per una lettera basata su dizionario dati, selezionare **Anteprima** > **Anteprima**. Oppure, per una lettera non basata su dizionario dati, selezionare **Anteprima**. È inoltre possibile passare il mouse su una lettera (senza selezionarla) e toccare l&#39;icona Anteprima lettera per visualizzarla in anteprima.

   >[!NOTE]
   >
   >Se un dizionario dati non è associato alla lettera, viene visualizzata l&#39;anteprima della lettera. In caso contrario, se la lettera è basata su un dizionario dati, Gestione corrispondenza visualizza le opzioni Anteprima e Personalizzato nel menu Anteprima ed è possibile selezionare una delle due opzioni. È inoltre possibile associare i dati del test a un dizionario dati. Quando al dizionario [dati sono associati dati](../../forms/using/data-dictionary.md#p-working-with-test-data-p)di test, quando si seleziona l&#39;opzione di anteprima viene visualizzata l&#39;anteprima normale con i dati di test popolati.

1. Per eseguire il rendering di una corrispondenza durante la visualizzazione in anteprima, è necessario essere un amministratore o parte di uno dei seguenti gruppi:

   * forms-users (per visualizzare l&#39;anteprima sull&#39;istanza di creazione)
   * cm-agent-users (per la rappresentazione nell’istanza di pubblicazione)

   Se non disponete delle autorizzazioni necessarie, richiedete all&#39;amministratore l&#39;accesso appropriato. Per ulteriori informazioni sulla creazione e l’aggiunta di utenti ai gruppi, consultate [Aggiunta di utenti o gruppi a un gruppo](/help/sites-administering/security.md). Se tentate di eseguire il rendering di una corrispondenza senza disporre delle autorizzazioni appropriate, viene visualizzata la pagina di errore 404.

1. Se avete selezionato **Anteprima** > **Personalizzato**, si apre una finestra di dialogo. Nella finestra di dialogo, selezionare un file di dati corrispondente al dizionario dati con cui visualizzare l&#39;anteprima della lettera, quindi selezionare **Anteprima**. Un file di dati viene creato in base a un dizionario dati per una lettera specifica. Per ulteriori informazioni sul file di dati, vedere [Dizionario](../../forms/using/data-dictionary.md#p-working-with-test-data-p)dati.

   ![Anteprima lettera](assets/8_previewcustomdatafile.png)

1. L&#39;anteprima HTML della lettera (anteprima moduli mobili) si apre con la scheda Dati attivata per impostazione predefinita.

   Per ulteriori informazioni sui moduli per dispositivi mobili e sulle relative funzioni, vedere Differenza tra le [funzioni di Mobile Forms e PDF forms](https://helpx.adobe.com/livecycle/help/mobile-forms/feature-differentiation-mobile-forms-pdf.html).

   Sono disponibili tre schede: dati, contenuto e allegati. Se non sono presenti elementi di dati (variabili segnaposto e campi di layout), la lettera si apre direttamente con la scheda Contenuto visualizzata. La scheda Allegati è disponibile solo quando gli allegati sono presenti o l&#39;accesso alla libreria è abilitato.

   >[!NOTE]
   >
   >Per ulteriori informazioni sul passaggio tra la modalità di rappresentazione HTML o PDF dell&#39;anteprima della lettera, vedere [Modificare la modalità di rappresentazione della lettera](#changerenditionmode). Per ulteriori informazioni sul supporto PDF in Gestione e AEM corrispondenza, consultate [Discontinuità dei plug-in del browser NPAPI e relativo impatto](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html) e [PDF forms a HTML5 Forms](https://helpx.adobe.com/aem-forms/kb/pdf-forms-to-html5-forms.html).

### Enter data {#enterdata}

Nella scheda Dati, compilare i campi e i segnaposto del layout disponibili.

1. Immettete i dati e le variabili di contenuto nei campi come necessario. Compilare tutti i campi obbligatori contrassegnati da un asterisco (*) per attivare il pulsante **Invia** .

   Toccate un valore del campo dati nell&#39;anteprima HTML della lettera per evidenziare il campo dati corrispondente nella scheda Dati.

   ![Immettere i dati nella lettera](assets/2_enterdata.png) ![2_1_enterdata](assets/2_1_enterdata.png)

### Gestione contenuto {#managecontent}

Nella scheda del contenuto, gestire il contenuto, ad esempio frammenti di documento e variabili di contenuto, nella lettera.

1. Select **Content**. Gestione corrispondenza visualizza la scheda del contenuto della lettera.

   ![Scheda Contenuto - Modulo evidenziazione nel contenuto](assets/3_content.png)

1. Modificate i moduli di contenuto, come necessario, nella scheda Contenuto. Per attivare il modulo di contenuto rilevante nella gerarchia dei contenuti, potete toccare la riga o il paragrafo pertinenti nell&#39;anteprima della lettera o toccare il modulo di contenuto direttamente nella gerarchia Contenuto.

   Ad esempio, la riga &quot;Abbiamo rivisto... &quot; è selezionato nell&#39;elemento grafico seguente e il relativo modulo contenuto è selezionato nella scheda Contenuto.

   ![4_highlightmoduleincontent](assets/4_highlightmoduleincontent.png)

   Nella scheda Contenuto o Dati, toccando Evidenzia moduli selezionati ( ![highlightmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) in alto a sinistra dell&#39;anteprima della lettera HTML, è possibile disabilitare o abilitare la funzionalità per passare al modulo di contenuto/dati quando il testo, il paragrafo o il campo di dati pertinenti sono selezionati nell&#39;anteprima della lettera.

   Per ulteriori informazioni sulle azioni disponibili per i vari moduli nell’interfaccia utente Crea corrispondenza, consultate [Azioni e informazioni disponibili nell’interfaccia](#actions-and-info-available-in-the-create-correspondence-content-tab)utente Crea corrispondenza.

1. Per individuare i moduli di contenuto, utilizzare il campo Trova. Immettete il nome o il titolo completo o parziale del modulo di contenuto per la ricerca nella corrispondenza.
1. Toccate l&#39;icona Visualizza ( ![visualizzazione](assets/display.png)) davanti a un elenco, un testo, una condizione o un&#39;area di destinazione per visualizzarla o nasconderla nella lettera.
1. Per modificare un modulo di testo in linea o modificabile, toccate l&#39;icona **Modifica** (modulo ![edittextmodule](assets/edittextmodule.png)) o fate doppio clic sul modulo di testo corrispondente nell&#39;anteprima della lettera.

   Il sistema visualizza un editor di testo per modificare e formattare il testo.

   Il correttore ortografico predefinito nel browser esegue il controllo ortografia nell&#39;editor di testo. Per gestire il controllo ortografico e grammaticale, potete modificare le impostazioni del correttore ortografico del browser oppure installare plug-in/addons del browser per il controllo ortografico e grammaticale.

   È inoltre possibile utilizzare le varie scelte rapide da tastiera nell&#39;editor di testo per gestire, modificare e formattare il testo. Per ulteriori informazioni sulle scelte rapide da tastiera dell&#39;Editor [di](/help/forms/using/keyboard-shortcuts.md#correspondence-management) testo, vedere Scelte rapide da tastiera per la gestione della corrispondenza.

   ![5_edittextmodule](assets/5_edittextmodule.png)

   È possibile riutilizzare uno o più paragrafi di testo presenti in un&#39;altra applicazione del documento. Potete copiare e incollare direttamente il testo, ad esempio da MS Word, pagine HTML o qualsiasi altra applicazione.

   È possibile copiare e incollare uno o più paragrafi di testo in un modulo di testo modificabile. Ad esempio, è possibile che si disponga di un documento MS Word con un elenco puntato di prove di residenza accettabili, come segue:

   ![pastetextmspada](assets/pastetextmsword.png)

   È possibile copiare e incollare direttamente il testo dal documento di Microsoft Word a un modulo di testo modificabile. La formattazione, ad esempio l&#39;elenco puntato, il font e il colore del testo, viene mantenuta nel modulo di testo.

   ![pastetexteditablemomodule](assets/pastetexteditablemodule.png)

   >[!NOTE]
   >
   >La formattazione del testo incollato, tuttavia, presenta alcune [limitazioni](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html).

   È possibile applicare un rientro al testo e ai numeri della lettera utilizzando il tasto Tab. Ad esempio, è possibile utilizzare il tasto Tab per allineare più colonne di testo in un elenco in un formato tabulare.

   ![tabspaces](assets/tabspaces.png)

   Esempio: Uso del tasto Tab per allineare più colonne di testo in un formato tabulare

   >[!NOTE]
   >
   >Per ulteriori informazioni sull&#39;impostazione della spaziatura tra le tabulazioni per i moduli di testo e le lettere, vedere [Ulteriori informazioni sull&#39;utilizzo della spaziatura tra le tabulazioni per disporre il testo](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).

1. Se necessario, inserire caratteri speciali nella corrispondenza. Ad esempio, è possibile utilizzare la palette Caratteri speciali per inserire:

   * Simboli di valuta come €,⇒ e £
   * Simboli matematici come i simboli all&#39;unisono, seguente:
   * Simboli di punteggiatura come ‟ e&quot;

   ![caratteri speciali](assets/specialcharacters.png)

   La gestione della corrispondenza è dotata di supporto per 210 caratteri speciali. L&#39;amministratore può [aggiungere il supporto per più o meno caratteri speciali personalizzati in base alla personalizzazione](../../forms/using/custom-special-characters.md).

1. Per evidenziare\enfatizzare parti di testo in un modulo in linea modificabile, selezionate il testo e toccate Colore evidenziazione.

   ![letterbackground, colore](assets/letterbackgroundcolor.png)

   È possibile toccare direttamente un colore di base `**[A]**` presente nella palette Colori base oppure toccare **Seleziona** dopo aver utilizzato il cursore `**[B]**` per scegliere l&#39;ombreggiatura appropriata del colore.

   Facoltativamente, potete anche passare alla scheda Avanzate per selezionare la tonalità, la luminosità e la saturazione appropriata `**[C]**` per creare il colore preciso, quindi toccare Seleziona `**[D]**` per applicare il colore per evidenziare il testo.

   ![textbackground, colore](assets/textbackgroundcolor.png)

1. Apportate le modifiche appropriate al contenuto e al formato, quindi toccate **Salva**. Toccate ( ![editnextmoduleccr](assets/editnextmoduleccr.png)) per passare da un modulo di testo modificabile all&#39;altro oppure toccate **Salva e Avanti** per salvare le modifiche e passare al successivo modulo di testo modificabile.
1. Il sistema visualizza anche le variabili non compilate per ciascuno dei rami. In assenza di variabili non compilate, le variabili non compilate vengono visualizzate come 0. Se è presente una variabile non compilata, potete toccare un ramo per espanderla e individuare la variabile non compilata. Utilizzate la barra degli strumenti del contenuto per eliminare il contenuto, aumentare/diminuire il rientro del contenuto e inserire interruzioni di pagina prima/dopo il contenuto.

   È possibile inserire interruzioni di pagina sopra e sotto i moduli dati anche quando fanno parte di elenchi e condizioni.

1. Toccate Apri/Chiudi variabile di contenuto (variabili di contenuto ![open contentvariables](assets/opencontentvariables.png)) per aprire le variabili di contenuto e compilarle correttamente.
1. Una volta compilata correttamente la variabile non compilata, il conteggio della variabile non compilata è impostato su 0.

   Nell&#39;interfaccia utente Crea corrispondenza, il conteggio delle variabili non compilate viene visualizzato a ogni livello della gerarchia di qualsiasi modulo che contiene almeno una variabile. Se un modulo contiene variabili non compilate, il conteggio viene visualizzato a livello di variabile, modulo, area di destinazione e modello di lettera.

   Il conteggio delle variabili non compilate include:

   * Solo variabili dizionario dati e segnaposto non protette. Il conteggio delle variabili non include variabili di layout o dizionario dati protetti.
   * Campi obbligatori.
   * Campi di layout se sono obbligatori e associati all’utente.
   * Solo istanze di variabili univoche. Se un modulo, un&#39;area di destinazione o un modello di lettera contiene due o più istanze della stessa variabile, il conteggio viene visualizzato come 1 (uno). Tuttavia, per ciascuna istanza, il conteggio viene visualizzato come 1.

   Il conteggio delle variabili non compilate non include i moduli deselezionati. Se un modulo è incluso in un modello di lettera ma non è nella lettera, il conteggio delle variabili non compilate in questo modulo non viene visualizzato.

   Per l&#39;area di destinazione, il modulo e la variabile il conteggio viene visualizzato a destra di ciascun oggetto nel modello lettera. Tuttavia, per il modello completo, il conteggio viene visualizzato nella barra di stato Crea corrispondenza.

   I moduli in un modello di lettera visualizzano il conteggio delle variabili non compilate come descritto di seguito:

   * **Testo** Visualizza la somma delle variabili segnaposto univoche e degli elementi del dizionario dati non compilati contenuti nel modulo di testo.
   * **Condizione** Visualizza la somma delle variabili di condizione univoche non compilate contenute nella condizione e delle variabili contenute nei moduli risultanti.
   * **Elenco** Visualizza la somma di tutte le variabili univoche non compilate contenute nei moduli assegnati all&#39;elenco.
   * **Area** di destinazione Visualizza la somma di tutte le variabili univoche non compilate contenute nei moduli assegnati all&#39;area di destinazione.

   Per le variabili con valori predefiniti, tenete presente quanto segue:

   * Per impostazione predefinita, un campo di variabile booleana è *false*. Tuttavia, la variabile viene considerata non compilata. Ciò implica che il conteggio delle variabili include tutti i campi delle variabili booleane con valore *false*.

   * Per impostazione predefinita, un campo variabile numerica è *0 (zero)*. Tuttavia, la variabile viene considerata non compilata. Ciò implica che il conteggio delle variabili include tutti i campi delle variabili numeriche con valore *0 (zero)*.



#### Azioni e informazioni disponibili nella scheda Crea contenuto corrispondenza {#actions-and-info-available-in-the-create-correspondence-content-tab}

**Area di destinazione**

* Inserisci riga vuota: Inserisce una nuova riga vuota.
* Inserisci testo in linea: Inserisce un nuovo modulo di testo.
* Blocco ordine (info): Indica che l’ordine dei contenuti non può essere modificato.
* Valori non compilati (info): Indica il numero di variabili non compilate nell&#39;area di destinazione.

**Modulo**

* Selezione (icona occhio): Include\esclude il modulo dalla lettera.
* Skip Bullets (applicabile per i moduli elenco e i relativi moduli figlio): Ignora i punti elenco in un particolare modulo.
* Interruzione di pagina prima (applicabile per i moduli figlio dell&#39;area di destinazione): Inserisce un&#39;interruzione di pagina prima del modulo.
* Interruzione di pagina dopo (applicabile per i moduli figlio dell&#39;area di destinazione): Inserisce un&#39;interruzione di pagina prima del modulo.
* Valori non compilati (info): Indica il numero di variabili non compilate nell&#39;area di destinazione.
* Modifica (solo moduli di testo): Aprite l’editor Rich Text per modificare il modulo di testo.
* Pannello dati (moduli di testo e condizione): Aprite tutte le variabili del modulo.

**Modulo elenco**

* Inserisci riga vuota: Inserisce una nuova riga vuota.
* Libreria contenuto: Apre la libreria Contenuto per aggiungere moduli all&#39;elenco.
* Impostazione elenco (solo elenco nidificato):
* Blocco ordine (info): Indica che l&#39;ordine delle voci dell&#39;elenco non può essere modificato.

### Gestire gli allegati {#manage-attachments}

1. Selezionare **Allegati**. Gestione corrispondenza visualizza gli allegati disponibili, così come impostati durante la creazione del modello di lettera.
1. È possibile scegliere di non inviare un allegato insieme alla lettera toccando l&#39;icona della vista e toccando la croce nell&#39;allegato per eliminarla dalla lettera. Per gli allegati specificati, durante la creazione di un modello di lettera, come Obbligatorio, le icone Visualizza ed Elimina sono disattivate.
1. Toccate l&#39;icona Accesso ![libreria (accesso](assets/libraryaccess.png)libreria) per accedere alla libreria Contenuto per inserire risorse DAM come allegati.

   >[!NOTE]
   >
   >L&#39;icona Accesso libreria è disponibile solo l&#39;accesso alla libreria era abilitato durante la creazione della lettera.

1. Se l&#39;ordine degli allegati non è stato bloccato durante la creazione della corrispondenza, è possibile riordinare gli allegati selezionando un allegato e toccando le frecce verso il basso e verso l&#39;alto.

   Per ulteriori informazioni, vedere Consegna [](#attachmentdelivery)allegati.

### Gestire il contenuto in anteprima e inviare la lettera {#manage-content-in-preview-and-submit-the-letter}

È possibile apportare modifiche al layout e al contenuto per garantire che la lettera abbia l&#39;aspetto desiderato e inviarla ai vari processi post.

1. Per evidenziare tutto il contenuto modificabile nella lettera, toccate **Evidenzia sezioni** modificabili.

   Il contenuto modificabile della lettera viene evidenziato con sfondo grigio.

   ![Evidenzia contenuto modificabile](assets/4_highlightmoduleincontent-1.png)

1. Modificate i moduli di contenuto, come necessario, nella scheda Contenuto. Per attivare il modulo di contenuto rilevante nella gerarchia dei contenuti, potete toccare la riga o il paragrafo pertinenti nell&#39;anteprima della lettera o toccare il modulo di contenuto direttamente nella gerarchia Contenuto.

   Ad esempio, la riga &quot;Per consentirci di accedere...&quot; è selezionato nell&#39;immagine seguente e il modulo di contenuto corrispondente è selezionato nella scheda Contenuto.

   Toccando Evidenzia moduli selezionati nel contenuto ( ![evidenziati, modulesincontentccr](assets/highlightselectedmodulesincontentccr.png)), potete disattivare o abilitare la funzionalità per evidenziare il modulo contenuto nella scheda Contenuto quando il testo, il paragrafo o il campo dati pertinenti vengono toccati nell&#39;anteprima della lettera.

   Per ulteriori informazioni sulle azioni disponibili per i vari moduli nell’interfaccia utente Crea corrispondenza, consultate [Azioni e informazioni disponibili nell’interfaccia](#actions-and-info-available-in-the-create-correspondence-content-tab)utente Crea corrispondenza.

1. Per aggiungere un&#39;interruzione di pagina alla lettera, toccare il punto in cui si desidera inserire un&#39;interruzione di pagina e selezionare Interruzione di pagina prima o Interruzione di pagina dopo ( ![interruzione di pagina prima](assets/pagebreakbeforeafter.png)).

   Nella lettera viene inserito un segnaposto di interruzione di pagina esplicito. Per vedere in che modo un&#39;interruzione di pagina esplicita influisce sulla lettera, vedere l&#39;anteprima PDF appiattita.

   >[!NOTE]
   >
   >Poiché i moduli per dispositivi mobili non supportano le interruzioni di pagina, le intestazioni e i piè di pagina vengono visualizzati solo una volta. È tuttavia possibile impostare esplicitamente intestazioni e piè di pagina nel layout (per pagina) in modo che vengano visualizzati nell&#39;anteprima dei moduli per dispositivi mobili. Inoltre, le eventuali pagine vuote nella lettera non vengono visualizzate nell&#39;anteprima dei moduli per dispositivi mobili.

   ![Interruzione di pagina esplicita](assets/8_pagebreak.png)

1. Per salvare la lettera come bozza, su cui è possibile continuare a lavorare in un secondo momento, toccate Salva come bozza. Per utilizzare questa opzione, la lettera deve essere [pubblicata](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Per ulteriori informazioni, vedere Istanza bozza in [Salvataggio delle bozze e invio delle istanze](#savingdrafts)di lettere.

   ![saveasarola](assets/saveasdraft.png)

   Viene visualizzata la finestra di dialogo Nome lettera bozza con l&#39;ID dell&#39;istanza della lettera. Facoltativamente, puoi modificare questo ID. Prendete nota della lettera Id e toccate **Fine**. In seguito, potrete utilizzare questo ID per [ricaricare la lettera](submit-letter-topostprocess.md#reloaddraft)bozza.

1. Per visualizzare in anteprima la lettera come PDF appiattito con il layout preciso e le interruzioni di pagina che verranno inviate, toccate ( ![anteprima](assets/preview.png)) Anteprima.

   La lettera viene visualizzata come PDF appiattito. Il PDF appiattito è la rappresentazione esatta della lettera così come verrà inviata con i font, le interruzioni e il layout corretti della lettera.

   >[!NOTE]
   >
   >Se utilizzate Mozilla Firefox e il tipo di rappresentazione HTML, per visualizzare in anteprima la lettera come PDF appiattito, accertatevi di utilizzare il plug-in nativo del browser e non il plug-in  Acrobat. Per selezionare il plug-in del browser nativo, accedete alle impostazioni di Mozilla Firefox e, per il tipo di contenuto PDF, selezionate Anteprima in Firefox.

1. Se l’anteprima PDF appiattita è soddisfacente, toccate **Invia** per inviare la lettera. Oppure, per apportare modifiche alla lettera, toccate **Esci da anteprima** per tornare all’anteprima dell’interfaccia utente Crea corrispondenza della lettera e apportare modifiche alla lettera. Toccando Invia, se nell’istanza Pubblica è abilitata la configurazione Gestisci istanza lettera, viene generata l’istanza Invia lettera.

   Per ulteriori informazioni, vedere Istanza bozza in Salvataggio di bozze e invio di istanze di lettere.

   È inoltre possibile salvare la lettera come bozza per apportare modifiche alla lettera in un secondo momento.

   Dopo aver apportato le modifiche necessarie, potete inviare la lettera dall’anteprima HTML5 oppure toccare nuovamente Anteprima per controllare l’output PDF appiattito.

   Per informazioni sulle differenze tra moduli HTML5 e PDF forms, vedere Differenza tra [funzioni per moduli HTML5 e PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

## Salvataggio di bozze e invio di istanze di lettere {#savingdrafts}

Quando viene eseguito il rendering di una lettera nell&#39;interfaccia utente Crea corrispondenza, potete salvare la lettera come visualizzata.

È possibile salvare due tipi di istanze di lettere: Istanza bozza e Invia.

* **Istanza** bozza: L&#39;istanza Draft acquisisce lo stato corrente della lettera di cui si sta visualizzando l&#39;anteprima. Per salvare un&#39;istanza bozza, assicuratevi innanzitutto che la lettera e tutte le risorse a cui fa riferimento la lettera siano in stato Pubblicato. Per informazioni sulla pubblicazione di una lettera, consultate [Pubblicare una risorsa](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Prima di salvare la lettera come bozza, è necessario pubblicare una lettera, perché quando si pubblica una lettera si crea una versione della lettera, delle relative risorse dipendenti e dei dati in quel momento. La versione pubblicata di una lettera non può essere modificata dall’utente stesso o da un altro utente e può essere ripristinata in un secondo momento senza discrepanze impreviste dalla versione pubblicata. Potete tornare a questa istanza in un secondo momento e continuare da dove siete partiti.

* **Invia istanza**: Le istanze di invio acquisiscono lo stato della lettera durante l&#39;invio. L&#39;istanza Submit memorizza lo stato PDF dell&#39;istanza della lettera dopo che questa è stata elaborata insieme ai dati immessi dall&#39;utente nell&#39;interfaccia utente Create Correspondence.

Tali istanze possono essere salvate solo quando la lettera viene visualizzata nell’istanza di pubblicazione. Per impostazione predefinita, il salvataggio delle istanze è disattivato. Per abilitare il salvataggio delle istanze di lettere, eseguire le operazioni seguenti.

1. In AEM, aprite Adobe Experience Manager Web Console Configuration per il server utilizzando il seguente URL: https://&lt;server>:&lt;porta>/&lt;percorso contestuale>/system/console/configMgr
1. Individuate le configurazioni di **[!UICONTROL gestione della corrispondenza]** e fate clic su di essa.
1. Selezionate **[!UICONTROL Gestisci istanze lettera nella configurazione Pubblica]** , quindi fate clic su **[!UICONTROL Salva]**.

Quando il salvataggio delle istanze di lettera è attivato, è possibile selezionare la posizione in cui salvare le istanze di lettera. Esistono due opzioni per salvare le istanze della lettera: Salvataggio locale o salvataggio remoto.

### Salvataggio locale {#local-save}

Le istanze di lettere vengono salvate nell’istanza di pubblicazione e vengono replicate in modo inverso nell’istanza di creazione.

### Salvataggio remoto {#remote-save}

Questa opzione è disponibile per le persone che hanno dei dubbi sul salvataggio di dati utente in istanze pubblicate, che in genere si trovano al di fuori del firewall aziendale. Quando il salvataggio remoto è attivato, le istanze della lettera non vengono salvate nell’istanza di pubblicazione, ma vengono salvate in remoto nell’autore di elaborazione specificata dalle configurazioni SDK client LiveCycle.

#### Abilita salvataggio remoto {#enable-remote-save}

1. In AEM, aprite Adobe Experience Manager Web Console Configuration per il server utilizzando il seguente URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`
1. Cercate le configurazioni **[!UICONTROL di gestione della]** corrispondenza e fate clic su di essa.
1. Individuare la configurazione del salvataggio **** remoto, controllarla e fare clic su **[!UICONTROL Salva]**.

#### Specificare le impostazioni di elaborazione per l&#39;autore {#specify-processing-author-settings}

1. In AEM, aprite Adobe Experience Manager Web Console Configuration per il server utilizzando il seguente URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Configurazione della console Web Adobe Experience Manager](assets/2configmanager.png)

1. In questa pagina, individua  Adobe Configurazione SDK client per LiveCycli e espandi facendo clic su di esso.

1. Nell’URL del server di elaborazione, immettete il nome del server di LiveCycle, fornite le informazioni di accesso e fate clic su **Salva**.

   ![Immettere il nome e le informazioni di login del server di LiveCycle](assets/3configmanager.png)

1. Se necessario, impostate il nome utente e la password con cui desiderate accedere al server.

#### Consegna dell&#39;allegato {#attachmentdelivery}

* Gli allegati lettera sono disponibili nella fase di post-elaborazione del PDF, creata dopo l’invio delle lettere.
* Quando viene eseguito il rendering della lettera utilizzando le API lato server come PDF interattivo o non interattivo, il PDF renderizzato contiene allegati come allegati PDF.
* Quando un processo di post associato a un modello di lettera viene caricato nell’ambito delle operazioni di invio o completamento della corrispondenza tramite l’interfaccia utente Crea corrispondenza, gli allegati vengono passati come il parametro List&lt;com.adobe.idp.Document> nel parametro AttachmentDocs.
* I meccanismi di consegna forniti dall&#39;utente, come e-mail e stampa, forniscono anche allegati insieme al PDF della corrispondenza generata.

## Modalità di rappresentazione dell&#39;anteprima della lettera: Anteprima dei moduli mobili e anteprima PDF {#rendition-modes-of-letter-preview-mobile-forms-preview-and-pdf-preview}

 AEM Forms Correspondence Management visualizza una lettera come HTML nell&#39;interfaccia utente Crea corrispondenza. Tuttavia, la gestione della corrispondenza continua a supportare il ripristino dell&#39;anteprima PDF invece dell&#39;anteprima HTML. Per ulteriori informazioni sul passaggio tra la modalità di anteprima HTML e PDF, consultate [Modificare la modalità di rappresentazione della lettera](#changerenditionmode).

Di seguito sono riportati i vantaggi e le funzionalità disponibili nell’anteprima HTML e PDF.

**Vantaggi dei moduli mobili/anteprima HTML**

* **Toccate un valore del campo di dati per evidenziare il campo** di dati corrispondente: Nell&#39;interfaccia utente Crea corrispondenza, è possibile toccare un valore del campo dati nella lettera per evidenziare il campo dati corrispondente nella scheda Dati. Per ulteriori informazioni, vedere [Immettere i dati](#enterdata).

* **Supporto** browser: Consente di rimuovere gradualmente il supporto per NPAPI, con effetto sull’anteprima PDF della lettera. L&#39;anteprima della lettera nei moduli HTML/mobili non viene modificata da questo problema.
* **Evidenziare il contenuto modificabile in una lettera**: Nell’interfaccia utente Crea corrispondenza, potete toccare Evidenzia contenuto modificabile per evidenziare in grigio tutto il contenuto modificabile della lettera. Per ulteriori informazioni, consultate [Gestire il contenuto](#managecontent).

`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`
`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`  **Vantaggi dell&#39;anteprima PDF**

* **Interruzione** pagina: Nell’anteprima PDF è possibile visualizzare esattamente in che modo le interruzioni di pagina nella lettera influiscono sul relativo output.
* **Anteprima** finale: Nell’anteprima PDF è possibile visualizzare la formattazione e l’aspetto esatti della lettera così come apparirà nell’output della stessa.

Per informazioni sul supporto degli script nei PDF forms, vedere [Supporto](https://help.adobe.com/en_US/livecycle/11.0/ScriptingSupport/index.html)script.

Per ulteriori informazioni sul supporto degli script nei moduli HTML5, vedere [Supporto degli script per i moduli](/help/forms/using/scripting-support.md)HTML5.

### Modifica della modalità di rappresentazione della lettera {#changerenditionmode}

Per impostazione predefinita, l’interfaccia utente Crea corrispondenza utilizza i moduli HTML o mobili per eseguire il rendering dell’anteprima della lettera. L&#39;anteprima dei moduli per dispositivi mobili non presenta problemi di rendering in alcun browser, in quanto utilizza il plug-in nativo del browser e non richiede plug-in aggiuntivi. È possibile modificare la modalità di anteprima della lettera in PDF. Tuttavia, i vincoli del browser possono creare problemi per le diverse funzioni dell&#39;anteprima PDF interattiva della lettera.

Per ulteriori informazioni sulla compatibilità del browser con l&#39;anteprima della lettera, consultate [Discontinuità dei plug-in del browser NPAPI e relativo impatto](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).

Per modificare la modalità di anteprima della lettera, completare i seguenti passaggi:

1. Vai a `https://[system]:'port'/system/console/configMgr` e, se necessario, accedi come Amministratore.
1. Accedete a **[!UICONTROL Corrispondence Management Configurations (Configurazioni]** di gestione corrispondenza) > **[!UICONTROL Rendition Type]** (Tipo **di rappresentazione) e selezionate** HTML Rendition **(Predefinito) o** PDF Rendition(RenderingPDF).
1. Fai clic su **[!UICONTROL Salva]**.

