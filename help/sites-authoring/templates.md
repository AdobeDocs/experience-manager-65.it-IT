---
title: 'Creazione di modelli di pagina  '
seo-title: 'Creazione di modelli di pagina  '
description: Un modello definisce la struttura della pagina risultante. Con l’Editor modelli, la creazione e manutenzione dei modelli non è più un’attività riservata agli sviluppatori.
seo-description: Un modello definisce la struttura della pagina risultante. Con l’Editor modelli, la creazione e manutenzione dei modelli non è più un’attività riservata agli sviluppatori.
uuid: e14cd298-289f-43f0-aacb-314ed5d56c12
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: b53348ca-fc50-4e7d-953d-b4c03a5025bb
docset: aem65
exl-id: 363b8fab-6ce7-4338-8478-3f25f2a1f117
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '4901'
ht-degree: 96%

---

# Creazione di modelli di pagina  {#creating-page-templates}

Quando si crea una pagina, è necessario selezionare un modello da utilizzare come base per la creazione della nuova pagina. Il modello definisce la struttura della pagina risultante, eventuali contenuti iniziali e i componenti che possono essere utilizzati.

Con l’**Editor modelli**, la creazione e la manutenzione dei modelli non è più un’attività che riguarda solo gli sviluppatori. Può essere coinvolto anche un tipo di “power user”, detto **autore dimodelli**. Gli sviluppatori devono comunque occuparsi di configurare l’ambiente, creare le librerie client e i componenti da utilizzare, ma una volta che questi elementi di base sono implementati, l’**autore del modello** avrà la flessibilità di creare e configurare i modelli senza un progetto di sviluppo.

Tramite la **Console dei modelli**, gli autori dei modelli possono:

* Creare un nuovo modello o copiarne uno esistente.
* Gestire il ciclo di vita del modello.

Tramite l’**Editor modelli**, gli autori dei modelli possono:

* Aggiungere componenti al modello e posizionarli su una griglia reattiva.
* Preconfigurare i componenti.
* Definire quali componenti possono essere modificati nelle pagine create con il modello.

Questo documento spiega come un **autore di modelli** può usare la console e l’editor per creare e gestire modelli modificabili.

Per informazioni dettagliate su come funzionano i modelli modificabili a livello tecnico, consulta il documento per sviluppatori [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md).

>[!NOTE]
>
>L’**Editor modelli** non supporta il targeting diretto a livello di modello. È possibile impostare come destinazione le pagine create in base a un modello modificabile, ma non i modelli stessi.

>[!CAUTION]
>
>Le pagine e i modelli creati con la **Console modelli** non sono destinati all’uso con l’interfaccia classica e tale uso non è supportato.

## Prima di iniziare {#before-you-start}

>[!NOTE]
>
>Un amministratore deve configurare una cartella di modelli nel **browser delle configurazioni** e applicare le autorizzazioni appropriate prima che un autore possa creare un modello in tale cartella.

Prima di iniziare, è importante considerare i seguenti aspetti:

* La creazione di un nuovo modello richiede collaborazione. Per questo motivo per ogni attività è indicato il relativo [Ruolo.](#roles)

* A seconda di come è configurata l’istanza, può essere utile sapere che AEM ora fornisce [due tipi di modelli di base](/help/sites-authoring/templates.md#editable-and-static-templates). Questo non influisce sul modo in cui [si utilizza effettivamente un modello per creare una pagina](#using-a-template-to-create-a-page), ma influisce sul tipo di modello che è possibile creare e sul modo in cui una pagina si relaziona al suo modello.

### Ruoli {#roles}

La creazione di un nuovo modello tramite **Templates Console (Console modelli)** e **Editor modelli** richiede la collaborazione tra i seguenti ruoli:

* **Amministratore**:

   * Crea una nuova cartella per i modelli che richiede i diritti di `admin`.

   * Tali compiti possono spesso essere svolti anche da uno sviluppatore

* **Sviluppatore**:

   * Si concentra sui dettagli tecnici o interni
   * Deve avere esperienza con l’ambiente di sviluppo.
   * Fornisce all’autore del modello le informazioni necessarie.

* **Autore del modello**:

   * Questo è un autore specifico che è membro del gruppo `template-authors`

      * In questo modo vengono assegnati i privilegi e le autorizzazioni necessarie.
   * Può configurare l’uso di componenti e altri dettagli di alto livello che richiedono:

      * Alcune conoscenze tecniche

         * Ad esempio, l’uso di schemi ricorrenti quando si definiscono i percorsi.
      * Informazioni tecniche fornite dallo sviluppatore.



A causa della natura di alcune attività, come la creazione di una cartella, è necessario un ambiente di sviluppo, e questo richiede conoscenza ed esperienza.

I compiti descritti nel presente documento sono elencati con il ruolo di responsabilità per il loro svolgimento.

### Modelli modificabili e statici {#editable-and-static-templates}

AEM offre ora due tipi di modelli di base:

* [Modelli modificabili](/help/sites-authoring/templates.md#creatingandmanagingnewtemplates)

   * Possono essere [creati](#creatinganewtemplate) e [modificati](#editingatemplate) dagli autori di modelli usando la console e l’editor **Modelli**. La console **Modelli** è accessibile nella sezione **Generale** della console **Strumenti**.

   * Dopo la creazione della nuova pagina, viene mantenuta una connessione dinamica tra la pagina e il modello. Le modifiche alla struttura del modello e/o al contenuto bloccato verranno quindi applicate a tutte le pagine create con questo modello. Le modifiche apportate al contenuto sbloccato (cioè iniziale) non verranno applicate.
   * I criteri per i contenuti, che è possibile definire dall’Editor modelli, permettono di applicare proprietà di progettazione persistenti. La modalità di progettazione nell’editor di pagine non viene più utilizzata per i modelli modificabili.

* Modelli statici

   * I modelli statici sono disponibili da diverse versioni di AEM.
   * Sono [forniti dagli sviluppatori](/help/sites-developing/page-templates-static.md), e non possono essere creati o modificati dagli autori.
   * Vengono copiati per creare una nuova pagina, ma non esiste alcuna connessione dinamica (il nome del modello viene registrato solo a titolo informativo).
   * La [modalità Progettazione](/help/sites-authoring/default-components-designmode.md) di applicare proprietà di progettazione persistenti.
   * Poiché la modifica di modelli statici è compito esclusivo di uno sviluppatore, consulta il documento per sviluppatori [Modelli di pagina - Statici](/help/sites-developing/page-templates-static.md) per ulteriori informazioni.

Per definizione, la console e l’editor dei modelli consentono di creare e modificare solo i modelli modificabili. Pertanto questo documento si concentra esclusivamente sui modelli modificabili.

### Utilizzo di un modello per creare una pagina {#using-a-template-to-create-a-page}

Quando si utilizza un modello per [creare una nuova pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page), non vi è alcuna differenza visibile e nessuna indicazione tra modelli statici e modificabili. Per l’autore della pagina, il processo è trasparente.

## Creazione e gestione di modelli {#creating-and-managing-templates}

Durante la creazione di un nuovo modello modificabile:

* Utilizza la console dei **Modelli**. Questa funzione è disponibile nella sezione **Generale** della console degli **Strumenti**.

   * Oppure direttamente da: [https://localhost:4502/libs/wcm/core/content/sites/templates.html/conf](https://localhost:4502/libs/wcm/core/content/sites/templates.html/conf)

* Se necessario, puoi [creare una cartella per i modelli](#creating-a-template-folder-admin).
* [Crea un nuovo modello](#creatinganewtemplateauthor), che sarà inizialmente vuoto.

* Se necessario, [definisci proprietà aggiuntive](#definingtemplatepropertiesauthor) per il modello.
* [Modifica il modello](#editingtemplates) per definire i seguenti elementi:

   * [Struttura](#editingatemplatestructureauthor): contenuto predefinito che non può essere modificato nelle pagine create con il modello.
   * [Contenuto iniziale](#editing-a-template-initial-content-author): contenuto predefinito che potrà essere modificato nelle pagine create con il modello.
   * [Layout](#editingatemplatelayoutauthor): per una vasta gamma di dispositivi.
   * [Stili](/help/sites-authoring/style-system.md): definisci gli stili da utilizzare con il modello e i suoi componenti.

* [Attiva il modello](#enablingatemplateauthor) per l’uso durante la creazione di una pagina.
* [Consenti il modello](#allowing-a-template-author) per la pagina o la sezione richiesta del sito web.
* [Pubblica il modello](#publishingatemplateauthor) per renderlo disponibile nell’ambiente di pubblicazione.

>[!NOTE]
>
>I **Modelli consentiti** sono spesso predefiniti al momento della configurazione iniziale del sito web.

>[!CAUTION]
>
>Non inserire mai informazioni che devono essere [internazionalizzate](/help/sites-developing/i18n.md) in un modello. A scopo di internalizzazione, si consiglia di utilizzare le [funzioni di localizzazione dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) .

### Creazione di una cartella di modelli - Amministratore {#creating-a-template-folder-admin}

È necessario creare una cartella di modelli per il progetto, che conterrà i modelli specifici per il progetto. Si tratta di un’operazione amministrativa descritta nel documento [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md#template-folders).

### Creazione di un nuovo modello - Autore del modello {#creating-a-new-template-template-author}

1. Apri la **Console modelli** (da **Strumenti ->** **Generale**) e passa alla cartella desiderata.

   >[!NOTE]
   >
   >In un’istanza AEM standard la cartella **globale** esiste già nella console modelli. Questa contiene i modelli predefiniti e funge da fallback se nella cartella corrente non sono presenti criteri e/o tipi di modello.
   >
   >
   >Si consiglia di utilizzare una [cartella di modelli creata per il progetto](/help/sites-developing/page-templates-editable.md#template-folders).

1. Seleziona **Crea**, seguito da **Crea modello** per aprire la procedura guidata.

1. Scegli un **Tipo di modello**, quindi seleziona **Avanti**.

   >[!NOTE]
   >
   >I tipi di modello sono layout predefiniti e possono essere pensati come modelli per un modello. Questi sono predefiniti dagli sviluppatori o dall’amministratore di sistema. Per ulteriori informazioni consulta il documento per sviluppatori [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md#template-type).

1. Completa i **Dettagli modello**:

   * **Nome modello**
   * **Descrizione**

1. Seleziona **Crea**. Viene visualizzata una conferma; seleziona **Apri**[](#editingatemplate) per iniziare a modificare il modello o **Fine** per tornare alla console dei modelli.

   >[!NOTE]
   >
   >Quando viene creato un nuovo modello, questo viene contrassegnato come **Bozza** nella console, a indicare che non è ancora disponibile per l’uso da parte degli autori di pagine.

### Definizione delle proprietà del modello - Autore del modello   {#defining-template-properties-template-author}

Un modello può avere le seguenti proprietà:

* Immagine

   * Immagine da utilizzare come [miniatura del modello](/help/sites-authoring/templates.md#template-thumbnail-image) per facilitarne la selezione, ad esempio nella procedura guidata Crea pagina.

      * Può essere caricata
      * Può essere generata in base al contenuto del modello

* Titolo

   * Titolo utilizzato per identificare il modello, ad esempio nella procedura guidata **Crea pagina**.

* Descrizione

   * Una descrizione opzionale per fornire informazioni sul modello e sul suo utilizzo, che possono essere visualizzate, ad esempio, nella procedura guidata **Crea pagina**.

Per visualizzare e/o modificare le proprietà:

1. Nella **console Modelli**, seleziona il modello.
1. Seleziona **Visualizza proprietà** dalla barra degli strumenti o le opzioni rapide per aprire la finestra di dialogo.
1. Ora è possibile visualizzare o modificare le proprietà del modello.

>[!NOTE]
>
>I modelli sono strumenti potenti per semplificare il flusso di lavoro di creazione delle pagine. Tuttavia, troppi modelli possono sopraffare gli autori e confondere la creazione di pagine. Una buona regola è mantenere il numero di modelli sotto i 100.
>
>Adobe consiglia di non disporre di più di 1000 modelli a causa di potenziali impatti sulle prestazioni.

>[!NOTE]
>
>Lo stato di un modello (bozza, attivato o disattivato) è indicato nella console.

#### Immagine della miniatura del modello {#template-thumbnail-image}

Per definire la miniatura del modello:

1. Modifica le proprietà del modello.
1. Scegli se caricare una miniatura o generarla dal contenuto del modello.

   * Per caricare una miniatura, tocca o fai clic su **Carica immagine**.
   * Per generare una miniatura, tocca o fai clic su **Genera anteprima**.

1. Per entrambi i metodi verrà visualizzata un’anteprima della miniatura.

   Se non è soddisfacente, tocca o fai clic su **Cancella** per caricare un’altra immagine o rigenerare l’anteprima.

1. Una volta ottenuta la miniatura desiderata, tocca o fai clic su **Salva e chiudi**.

### Abilitazione e autorizzazione di un modello - Autore del modello   {#enabling-and-allowing-a-template-template-author}

Per poter utilizzare un modello quando si crea una pagina, è necessario svolgere le seguenti operazioni:

* [Attiva i modelli](#enablingatemplate) per renderli disponibili per l’uso durante la creazione di pagine.
* [Consenti ai modelli](#allowingatemplate) di specificare i rami di contenuto in cui è possibile utilizzare il modello.

#### Abilitazione di un modello - Autore del modello {#enabling-a-template-template-author}

Un modello può essere attivato o disattivato per renderlo disponibile o non disponibile nella procedura guidata **Crea pagina**.

>[!CAUTION]
>
>Una volta abilitato un modello, verrà visualizzato un avviso quando un autore inizia ad aggiornarlo ulteriormente. In tal modo l’utente viene informato di un potenziale riferimento al modello, e che eventuali modifiche potrebbero quindi influenzare le pagine che vi fanno riferimento.

1. Nella **console Modelli**, seleziona il modello.
1. Seleziona **Abilita** o **Disabilita** nella barra degli strumenti e di nuovo nella finestra di dialogo di conferma.
1. È ora possibile utilizzare il modello quando si [crea una nuova pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page), anche se probabilmente si vorrà [modificare il modello](#editingatemplate) in base a specifiche esigenze.

>[!NOTE]
>
>Lo stato di un modello (bozza, attivato o disattivato) è indicato nella console.

#### Consentire un modello - Autore {#allowing-a-template-author}

Un modello può essere reso disponibile o non disponibile per alcuni rami di pagina.

1. Apri le [Proprietà pagina](/help/sites-authoring/editing-page-properties.md) per la pagina principale del ramo in cui desideri rendere disponibile il modello.

1. Apri la scheda **Avanzate**.

1. In **Impostazioni modello** utilizza **Aggiungi campo** per specificare il percorso del modello.

   Il percorso può essere esplicito o utilizzare schemi ricorrenti. Esempio:

   `/conf/<your-folder>/settings/wcm/templates/.*`

   L’ordine dei percorsi è irrilevante; tutti i percorsi vengono scansionati e gli eventuali modelli recuperati.

   >[!NOTE]
   >
   >Se l’elenco dei **Modelli consentiti** viene lasciato vuoto, l’albero viene asceso fino a quando non viene trovato un valore o un elenco.
   >
   >
   >Consulta [Disponibilità dei modelli](/help/sites-developing/templates.md#template-availability) - i principi per i modelli consentiti rimangono gli stessi.

1. Fai clic su **Salva** per salvare le modifiche alle proprietà della pagina.

>[!NOTE]
>
>Spesso i modelli consentiti sono predefiniti per l’intero sito quando è configurato.

### Pubblicazione di un modello - Autore del modello {#publishing-a-template-template-author}

Poiché al modello viene fatto riferimento quando viene eseguito il rendering di una pagina, il modello completamente configurato deve essere pubblicato in modo che sia disponibile nell’ambiente di pubblicazione.

1. Nella **console Modelli**, seleziona il modello.
1. Seleziona **Pubblica** nella barra degli strumenti per aprire la procedura guidata.
1. Seleziona **Criteri per contenuto** da pubblicare in tandem.

1. Seleziona **Pubblica** nella barra degli strumenti per completare l’azione.

## Modifica dei modelli - Autori dei modelli   {#editing-templates-template-authors}

Quando si crea o si modifica un modello, è possibile definire vari aspetti. La modifica dei modelli è simile alla creazione delle pagine.

È possibile modificare i seguenti aspetti di un modello:

* [Struttura](#editingatemplatestructure)

   I componenti aggiunti qui non possono essere spostati o rimossi dalle pagine risultanti, dagli autori delle pagine. Se si desidera permettere agli autori delle pagine di aggiungere e rimuovere componenti alle pagine risultanti, è necessario aggiungere un sistema di paragrafi al modello.

   Quando i componenti sono bloccati, è possibile aggiungere contenuti e questi ultimi possono essere modificati dagli autori delle pagine. È possibile sbloccare i componenti per consentire la definizione del [Contenuto iniziale](#editingatemplateinitialcontent).

   >[!NOTE]
   >
   >In modalità Struttura, tutti i componenti che sono l’elemento padre di un componente sbloccato non possono essere spostati, tagliati o cancellati.

* [Contenuto iniziale](#editingatemplateinitialcontent)

   Quando un componente è stato sbloccato, è possibile definire il contenuto iniziale che verrà copiato nelle pagine risultanti, create dal modello. I componenti sbloccati possono essere modificati nella pagina o nelle pagine risultanti.

   >[!NOTE]
   >
   >Nella modalità **Contenuto iniziale** e nelle pagine risultanti, tutti i componenti sbloccati che hanno un elemento padre accessibile (ad esempio i componenti all’interno di un contenitore di layout) possono essere eliminati.

* [Layout](#editingatemplatelayout)

   Qui è possibile predefinire il layout del modello per i formati di dispositivo richiesti. La modalità **Layout** per la creazione dei modelli ha le stesse funzionalità della modalità [**Layout** per la creazione delle pagine.](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)

* [Criteri di pagina](#editingatemplatepagepolicies)

   Sotto Criteri di pagina è possibile collegare alla pagina i criteri di pagina predefiniti. I criteri di pagina definiscono le varie configurazioni di progettazione.

* [Stili](/help/sites-authoring/style-system.md)

   Il sistema di stili consente all’autore del modello di definire le classi di stile nel criterio del contenuto di un componente, in modo che un autore di contenuti possa sceglierli quando modifica un componente in una pagina. Gli stili possono essere varianti visive alternative di un componente, per renderlo più flessibile.

   Per ulteriori informazioni, consulta la [documentazione sul sistema di stili](/help/sites-authoring/style-system.md).

Il selettore **Modalità** nella barra degli strumenti consente di selezionare e modificare l’aspetto appropriato del modello:

* [Struttura](#editingatemplatestructure)
* [Contenuto iniziale](#editingatemplateinitialcontent)
* [Layout](#editingatemplatelayout)

![chlimage_1-133](assets/chlimage_1-133.png)

L’opzione **Criterio pagina** nel menu **Informazioni pagina** consente invece di [selezionare i criteri di pagina richiesti](#editingatemplatepagepolicies):

![screen_shot_2018-03-23at120604](assets/screen_shot_2018-03-23at120604.png)

>[!CAUTION]
>
>Se un autore inizia a modificare un modello che è già stato abilitato, verrà visualizzato un avviso. In tal modo l’utente viene informato di un potenziale riferimento al modello, e che eventuali modifiche potrebbero quindi influenzare le pagine che vi fanno riferimento.

### Modifica di un modello - Struttura - Autore del modello {#editing-a-template-structure-template-author}

In modalità **Struttura** si definiscono i componenti e i contenuti per il modello, nonché i criteri per il modello e i suoi componenti.

* I componenti definiti nella struttura del modello non possono essere spostati su una pagina risultante, né eliminati da alcuna pagina risultante.
* Se desideri che gli autori delle pagine siano in grado di aggiungere e rimuovere componenti, aggiungi un sistema di paragrafi al modello.
* I componenti possono essere sbloccati e bloccati di nuovo per consentire di definire il [contenuto iniziale](#editingatemplateinitialcontent).

* Vengono definiti i criteri di design per i componenti e la pagina.

![screen_shot_2018-03-23at120819](assets/screen_shot_2018-03-23at120819.png)

In modalità **Struttura** dell’Editor modelli:

* **Aggiungi componenti**

   Ci sono diversi meccanismi per aggiungere componenti ai modelli:

   * Dal browser **Componenti** nel pannello laterale.
   * Utilizzando l’opzione **Inserisci componente** (icona **+**) nella barra degli strumenti dei componenti già presenti nel modello, oppure il riquadro **Trascina qui i componenti**.

   * Trascinando una risorsa (dal browser **Risorse** nel pannello laterale) direttamente sul modello per generare il componente appropriato in situ.

   Una volta aggiunto, ogni componente è contrassegnato con:

   * Un bordo
   * Un marcatore che indica il tipo di componente
   * Un marcatore che indica se il componente è stato sbloccato

   >[!NOTE]
   >
   >Quando si aggiunge al modello un componente **Titolo** pronto per l’uso, questo conterrà la **struttura** di testo predefinita.
   >
   >
   >Se si modifica questa impostazione e si aggiunge un proprio testo, questo testo aggiornato verrà utilizzato quando si crea una pagina dal modello.
   >
   >
   >Se si lascia il testo (struttura) predefinito, il titolo predefinito corrisponde al nome della pagina risultante.

   >[!NOTE]
   >
   >Sebbene non sia identica, l’aggiunta di componenti e risorse a un modello ha molte somiglianze con azioni simili durante la [creazione di pagine](/help/sites-authoring/editing-content.md).

* **Azioni dei componenti**

   Una volta aggiunte al modello, esegui le azioni sui componenti. Ogni singola istanza ha una barra degli strumenti che permette di accedere alle azioni disponibili e che dipende dal tipo di componente.

   ![screen_shot_2018-03-23at120909](assets/screen_shot_2018-03-23at120909.png)

   Può anche dipendere dalle azioni intraprese, ad esempio se un criterio è stato associato al componente, in tal caso l’icona di configurazione del progetto diventa disponibile.

* **Modifica e Configura**

   Con queste due azioni è possibile aggiungere contenuti ai componenti.

* **Bordo per indicare la Struttura**

   Quando si lavora in modalità **Struttura**, un bordo arancione indica il componente attualmente selezionato. Una linea tratteggiata indica il componente padre.

   Ad esempio, nella schermata qui sotto, il componente **Testo** è selezionato all’interno di un **Contenitore di layout** (responsivegrid).

   ![chlimage_1-134](assets/chlimage_1-134.png)

* **Criteri e proprietà (Generali)**

   I criteri relativi ai contenuti (o alle progettazioni) definiscono le proprietà di progettazione (o design) di un componente. Ad esempio, i componenti disponibili o le dimensioni minime e massime. Questi sono applicabili al modello (e alle pagine create con tale modello).

   Crea un criterio per i contenuti o selezionane uno esistente per un componente. In questo modo è possibile definire i dettagli del progetto.

   ![chlimage_1-135](assets/chlimage_1-135.png) ![chlimage_1-136](assets/chlimage_1-136.png)

   La finestra di configurazione è divisa in due parti.

   * Nella parte sinistra, in **Criteri**, è possibile selezionare un criterio esistente.
   * Nella parte destra, in **Proprietà** è possibile impostare le proprietà specifiche del tipo di componente.

   Le proprietà disponibili dipendono dal componente selezionato. Ad esempio, per un componente di testo, le proprietà definiscono, tra le altre opzioni, quelle di copia e incolla, formattazione e stile del paragrafo.

   ***Criterio***

   I criteri relativi ai contenuti (o alle progettazioni) definiscono le proprietà di progettazione (o design) di un componente. Ad esempio, i componenti disponibili o le dimensioni minime e massime. Questi sono applicabili al modello (e alle pagine create con tale modello).

   In **Criterio** puoi selezionare un criterio esistente da applicare al componente tramite il menu a discesa.

   ![chlimage_1-137](assets/chlimage_1-137.png)

   Puoi aggiungere un nuovo criterio selezionando il pulsante di aggiunta accanto al menu a discesa **Seleziona criterio**. Quindi devi assegnare un nuovo titolo nel campo **Titolo criterio**.

   ![chlimage_1-138](assets/chlimage_1-138.png)

   Il criterio esistente selezionato nel menu a discesa **Seleziona criterio** può essere copiato come nuovo criterio utilizzando il pulsante Copia, accanto al menu a discesa. Quindi devi assegnare un nuovo titolo nel campo **Titolo criterio**. Per impostazione predefinita, il criterio copiato si chiama **Copia di X**, dove X è il titolo del criterio da cui è stato copiato.

   ![chlimage_1-139](assets/chlimage_1-139.png)

   La descrizione del criterio nel campo **Descrizione criterio** è facoltativa.

   Nella sezione **Altri modelli che utilizzano il criterio selezionato**, è possibile vedere facilmente quali altri modelli utilizzano i criteri selezionati nell’elenco a discesa **Seleziona criterio**.

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Se vengono aggiunti come contenuto iniziale più componenti dello stesso tipo, lo stesso criterio si applica a tutti i componenti. Questo riflette la stessa restrizione nella [**Modalità Progettazione** per i modelli statici](/help/sites-authoring/default-components-designmode.md).

   ***Proprietà***

   In **Proprietà** puoi definire le impostazioni del componente. Sono disponibili due schede:

   * Principale
   * Funzioni

   *Principale*

   Nella scheda **Principale** sono definite le impostazioni più importanti del componente.

   Ad esempio, per un componente immagine è possibile definire le larghezze consentite e abilitare il caricamento lento.

   Se per un’impostazione sono consentite più configurazioni, tocca o fai clic sul pulsante **Aggiungi** per aggiungerne un’altra.

   ![chlimage_1-141](assets/chlimage_1-141.png)

   Per rimuovere una configurazione, tocca o fai clic sul pulsante **Elimina** situato a destra della configurazione.

   Per rimuovere una configurazione, tocca o fai clic sul pulsante** Elimina**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

   *Funzioni*

   La scheda **Funzioni** consente di attivare o disattivare funzioni aggiuntive del componente.

   Ad esempio, per un componente immagine è possibile definire le proporzioni di ritaglio, gli orientamenti consentiti e se il caricamento è ammesso.

   ![chlimage_1-143](assets/chlimage_1-143.png)

   >[!CAUTION]
   >
   >In AEM i rapporti di ritaglio sono definiti come **altezza/larghezza**. Questo differisce dalla definizione tradizionale di larghezza/altezza, per ragioni di compatibilità con versioni precedenti. Gli utenti che creano le pagine non noteranno alcuna differenza, purché sia stato definito chiaramente il **Nome**, che verrà visualizzato nell’interfaccia utente.

   >[!NOTE]
   >
   >[](/help/sites-administering/rich-text-editor.md#main-pars-header-206036638)I criteri dei contenuti per i componenti che si avvalgono dell’editor Rich Text possono essere definiti solo per le opzioni disponibili mediante tale editor tramite le impostazioni di interfaccia utente. [](/help/sites-administering/rich-text-editor.md#main-pars_header_206036638) [](/help/sites-administering/rich-text-editor.md#main-pars_header_206036638)

* **Criteri e proprietà (contenitore di layout)**

   Le impostazioni di criteri e proprietà di un contenitore di layout sono simili a quelle di uso generale, ma con alcune differenze.

   >[!NOTE]
   >
   >La configurazione di un criterio è obbligatoria per i componenti contenitore, in quanto consente di definire i componenti che saranno disponibili nel contenitore.

   La finestra di configurazione è divisa in due, come la finestra per uso generale.

   ***Criterio***

   I criteri relativi ai contenuti (o alle progettazioni) definiscono le proprietà di progettazione (o design) di un componente. Ad esempio, i componenti disponibili o le dimensioni minime e massime. Questi sono applicabili al modello (e alle pagine create con tale modello).

   In **Criterio** puoi selezionare un criterio esistente da applicare al componente tramite il menu a discesa. Questo funziona come nell’uso generale della finestra.

   ***Proprietà***

   In **Proprietà** è possibile scegliere quali componenti sono disponibili per il contenitore layout e definirne le impostazioni. Sono disponibili tre schede:

   * Componenti consentiti
   * Componenti standard
   * Impostazioni reattive

   *Componenti consentiti*

   Nella scheda **Componenti consentiti**, definisci quali componenti sono disponibili per il contenitore layout.

   * I componenti sono raggruppati in base ai gruppi di componenti, che possono essere espansi e ridotti.
   * Per selezionare tutti i componenti di un gruppo, attiva la casella del nome del gruppo; per deselezionare tutti i componenti di un gruppo, disattiva questa casella.
   * Se la casella contiene un meno (-) significa che è selezionato almeno un elemento del gruppo, ma non tutti.
   * È disponibile un sistema di ricerca per filtrare i componenti in base al nome.
   * Il numero a destra del nome di un gruppo di componenti indica quanti sono i componenti selezionati in tale gruppo, a prescindere dal filtro.

   ![chlimage_1-144](assets/chlimage_1-144.png)

   *Componenti standard*

   Nella scheda **Componenti standard**, definisci quali componenti vengono associati automaticamente a determinati tipi di file multimediali in modo che, quando un autore trascina una risorsa dal browser delle risorse, AEM sappia a quale componente associarla. Per questa configurazione sono disponibili solo componenti con zone di rilascio.

   Tocca o fai clic su **Aggiungi mappatura** per aggiungere un componente completamente nuovo e la mappatura del tipo MIME.

   Seleziona un componente nell’elenco e tocca o fai clic su **Aggiungi tipo** per aggiungere un altro tipo MIME a un componente già mappato. Fai clic sull’icona **Elimina** per rimuovere un tipo di MIME.

   ![chlimage_1-145](assets/chlimage_1-145.png)

   *Impostazioni reattive*

   Nella scheda **Impostazioni reattive** è possibile configurare il numero di colonne nella griglia risultante del contenitore layout.

* **Sblocca/Blocca componenti**

   Sblocca o blocca i componenti per definire se il contenuto è disponibile per la modifica in modalità **Contenuto iniziale**.

   Quando un componente è stato sbloccato:

   * Sul bordo è visualizzato un indicatore di lucchetto aperto.
   * La barra degli strumenti dei componenti verrà regolata di conseguenza.
   * I contenuti già inseriti non verranno più visualizzati in modalità **Struttura**.

      * Il contenuto già inserito è considerato contenuto iniziale ed è visibile solo nella modalità **Contenuto iniziale**.
   * L’elemento padre di un componente sbloccato non può essere spostato, tagliato o cancellato.

   ![chlimage_1-146](assets/chlimage_1-146.png)

   Ciò include lo sblocco di componenti contenitore in modo che possano essere aggiunti altri componenti, sia in modalità **Contenuto iniziale** che sulle pagine risultanti. Se hai già aggiunto componenti/contenuti al contenitore prima di sbloccarlo, questi non saranno più visualizzati in modalità **Struttura** ma saranno presenti in modalità **Contenuto iniziale**. In **Modalità struttura**, verrà mostrato solo il componente del contenitore stesso con il suo elenco di **Componenti consentiti**.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Per risparmiare spazio, il contenitore layout non cresce per accogliere l’elenco dei componenti consentiti. Piuttosto il contenitore diventa un elenco scorrevole.

   I componenti configurabili vengono visualizzati con l’icona **Policy**, che può essere toccata o su cui è possibile fare clic per modificare la policy e le proprietà del componente.

   ![chlimage_1-148](assets/chlimage_1-148.png)

* **Relazione con le pagine esistenti**

   Se la struttura viene aggiornata dopo la creazione di pagine basate sul modello, a tali pagine verranno applicate le modifiche apportate al modello. Questo fatto è segnalato da un avviso nella barra degli strumenti e da finestre di dialogo di conferma.

   ![chlimage_1-149](assets/chlimage_1-149.png)

### Modifica di un modello - Contenuto iniziale - Autore {#editing-a-template-initial-content-author}

La modalità **Contenuto iniziale** viene utilizzata per definire il contenuto che verrà visualizzato quando una pagina viene creata per la prima volta in base al modello. Il contenuto iniziale può quindi essere modificato dagli autori delle pagine.

Sebbene tutto il contenuto creato in modalità **Struttura** sia visibile nel **Contenuto iniziale**, solo i componenti sbloccati possono essere selezionati e modificati.

>[!NOTE]
>
>La modalità **Contenuto iniziale** è in pratica una modalità di modifica per le pagine create con quel modello. Pertanto, i criteri non vengono definiti in modalità **Contenuto iniziale**, ma in [**modalità Struttura**](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

* I componenti sbloccati disponibili per la modifica sono contrassegnati. Quando sono selezionati, hanno un bordo blu:

   ![chlimage_1-150](assets/chlimage_1-150.png)

* I componenti sbloccati dispongono di una barra degli strumenti che consente di modificare e configurare il contenuto:

   ![chlimage_1-151](assets/chlimage_1-151.png)

* Se un componente del contenitore è stato sbloccato (in modalità **Struttura**), è possibile aggiungervi nuovi componenti (in modalità **Contenuto iniziale**). I componenti aggiunti in modalità **Contenuto iniziale** possono essere spostati o eliminati dalle pagine risultanti.

   È possibile aggiungere un componente utilizzando l’area **Trascina qui i componenti** o l’opzione **Inserisci nuovo componente** dalla barra degli strumenti del contenitore appropriato.

   ![chlimage_1-152](assets/chlimage_1-152.png) ![chlimage_1-153](assets/chlimage_1-153.png)

* Se il contenuto iniziale del modello viene aggiornato dopo la creazione delle pagine basate sul modello, tali pagine non saranno influenzate dalle modifiche apportate al contenuto iniziale del modello.

>[!NOTE]
>
>Il contenuto iniziale è destinato alla preparazione dei componenti e del layout di pagina che fungono da punto di partenza per la creazione dei contenuti. Non è inteso come contenuto effettivo da mantenere così com’è. Per questo motivo, non può essere tradotto.
>
>Per includere nel modello il testo traducibile, ad esempio nelle intestazioni o nei piè di pagina, puoi utilizzare le funzioni di [localizzazione dei componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/get-started/localization.html).

### Modifica di un modello - Layout - Autore del modello {#editing-a-template-layout-template-author}

È possibile definire il layout del modello per una serie di dispositivi. Il [Layout reattivo](/help/sites-authoring/responsive-layout.md) per i modelli funziona come per la creazione delle pagine.

>[!NOTE]
>
>Le modifiche al layout verranno applicate in modalità **Contenuto iniziale**, ma non in modalità **Struttura**.

![chlimage_1-154](assets/chlimage_1-154.png)

### Modifica di un modello - Progettazione pagina - Autore/sviluppatore del modello {#editing-a-template-page-design-template-author-developer}

La progettazione della pagina, comprese le librerie lato client e le policy di pagina obbligatorie, viene mantenuta nell’opzione **Progettazione pagina** del menu **Informazioni pagina**.

Per accedere alla finestra di dialogo **Progettazione pagina**:

1. Dall&#39; **Editor modelli**, seleziona **Informazioni pagina** dalla barra degli strumenti, quindi **Progettazione pagina** per aprire la finestra di dialogo.
1. Si apre la finestra di dialogo **Progettazione pagina**, divisa in due sezioni:

   * Nella metà sinistra si definiscono i [criteri della pagina](/help/sites-authoring/templates.md#page-policies).
   * Nella metà destra si definiscono le [proprietà della pagina](/help/sites-authoring/templates.md#page-properties).

   ![chlimage_1-155](assets/chlimage_1-155.png)

#### Criteri di pagina {#page-policies}

È possibile applicare un criterio per i contenuti al modello o alle pagine risultanti. In tal modo si definiscono i criteri dei contenuti per il sistema di paragrafi principale della pagina.

![chlimage_1-156](assets/chlimage_1-156.png)

* Puoi selezionare un criterio esistente per la pagina dal menu a discesa **Seleziona criterio**.

   ![chlimage_1-157](assets/chlimage_1-157.png)

   Puoi aggiungere un nuovo criterio selezionando il pulsante di aggiunta accanto al menu a discesa **Seleziona criterio**. Quindi devi assegnare un nuovo titolo nel campo **Titolo criterio**.

   ![chlimage_1-158](assets/chlimage_1-158.png)

   Il criterio esistente selezionato nel menu a discesa **Seleziona criterio** può essere copiato come nuovo criterio utilizzando il pulsante Copia, accanto al menu a discesa. Quindi devi assegnare un nuovo titolo nel campo **Titolo criterio**. Per impostazione predefinita, il criterio copiato si chiama **Copia di X**, dove X è il titolo del criterio da cui è stato copiato.

   ![chlimage_1-159](assets/chlimage_1-159.png)

* Aggiungi un titolo al criterio nel campo **Titolo criterio**. Un criterio deve avere un titolo che permetta di riconoscerlo facilmente nel menu a discesa **Seleziona criterio**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

* La descrizione del criterio nel campo **Descrizione criterio** è facoltativa.
* Nella sezione **Altri modelli che utilizzano il criterio selezionato**, è possibile vedere facilmente quali altri modelli utilizzano i criteri selezionati nell’elenco a discesa **Seleziona criterio**.

   ![chlimage_1-161](assets/chlimage_1-161.png)

#### Proprietà pagina   {#page-properties}

Con le proprietà della pagina è possibile definire le librerie lato client richieste mediante la finestra di dialogo **Progettazione pagina**. Le librerie lato client includono fogli di stile e Javascript da caricare con il modello e le pagine create con tale modello.

![chlimage_1-162](assets/chlimage_1-162.png)

* Specifica le librerie lato client da applicare alle pagine create con questo modello. Immetti il nome di una libreria nel campo di testo nella sezione **Librerie lato client**.

   ![chlimage_1-163](assets/chlimage_1-163.png)

* Se sono necessarie più librerie, fai clic sul pulsante Aggiungi per aggiungere un ulteriore campo di testo al nome della libreria.

   ![chlimage_1-164](assets/chlimage_1-164.png)

   Aggiungi tutti i campi di testo necessari per le librerie lato client.

   ![chlimage_1-165](assets/chlimage_1-165.png)

* Se necessario, definisci la posizione relativa delle librerie trascinando i campi con la maniglia di trascinamento.

   ![chlimage_1-166](assets/chlimage_1-166.png)

>[!NOTE]
>
>L’autore del modello può specificare il criterio della pagina sul modello, ma dovrà ottenere i dettagli delle librerie appropriate lato client dallo sviluppatore.

### Modifica di un modello - Proprietà pagina iniziale - Autore {#editing-a-template-initial-page-properties-author}

L’opzione **Proprietà pagina iniziale** consente di definire le [proprietà della pagina iniziale](/help/sites-authoring/editing-page-properties.md) da utilizzare per la creazione delle pagine risultanti.

1. Dall’editor dei modelli, seleziona **Informazioni pagina** dalla barra degli strumenti, quindi **Proprietà pagina iniziale** per aprire la finestra di dialogo.

1. Nella finestra di dialogo è possibile definire le proprietà che si desidera applicare alle pagine create con questo modello.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Conferma le definizioni con **Fine**.

## Best practice   {#best-practices}

Quando si creano modelli, è necessario considerare i seguenti aspetti:

1. L’impatto delle modifiche apportate al modello, una volta che sono state create delle pagine da quel modello.

   Ecco un elenco delle diverse operazioni possibili sui modelli e di come influenzano le pagine create da essi:

   * Modifiche alla struttura:

      * Vengono immediatamente applicate alle pagine risultanti.
      * È comunque necessario pubblicare il modello modificato affinché i visitatori possano vedere le modifiche.
   * Modifiche ai criteri dei contenuti e alle configurazioni di progettazione:

      * Vengono applicate immediatamente alle pagine risultanti.
      * È necessario pubblicare le modifiche affinché i visitatori possano vederle.
   * Modifiche al contenuto iniziale:

      * Vengono applicate solo alle pagine create dopo la modifica del modello.
   * Le modifiche al layout dipendono dal ruolo del componente modificato:

      * Solo struttura: vengono applicate immediatamente.
      * Con contenuto iniziale: vengono applicate immediatamente solo alle pagine create dopo la modifica

   Si consiglia di prestare particolare attenzione nei seguenti casi:

   * Blocco o sblocco di componenti su modelli abilitati.
   * Questo può avere effetti collaterali, in quanto le pagine esistenti possono già essere in uso. In genere:

      * I componenti sbloccati (precedentemente bloccati) saranno assenti dalle pagine esistenti.
      * I componenti bloccati (che erano modificabili) nascondono il contenuto dalla visualizzazione sulle pagine.

   >[!NOTE]
   >
   >AEM fornisce avvisi espliciti quando si modifica lo stato di blocco di componenti su modelli che non sono più bozze.

1. [Creazione di cartelle personalizzate](#creatingatemplatefolderdeveloper) per i modelli specifici del sito.
1. [Pubblica i modelli](#publishingatemplateauthor) dalla console **Modelli**.
