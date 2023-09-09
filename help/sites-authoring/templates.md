---
title: Creazione di modelli di pagina
seo-title: Creating Page Templates
description: Il modello definisce la struttura della pagina risultante e, grazie all’editor di modelli, la creazione e la manutenzione dei modelli non è più un’attività che riguarda solo gli sviluppatori
seo-description: The template defines the structure of the resultant page and with the template editor, creating and maintaining templates is no longer a developer-only task
uuid: e14cd298-289f-43f0-aacb-314ed5d56c12
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: b53348ca-fc50-4e7d-953d-b4c03a5025bb
docset: aem65
exl-id: 363b8fab-6ce7-4338-8478-3f25f2a1f117
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '4864'
ht-degree: 80%

---

# Creazione di modelli di pagina  {#creating-page-templates}

Durante la creazione di una pagina è necessario selezionare un modello che verrà utilizzato come base per la creazione della nuova pagina. Il modello definisce la struttura della pagina risultante, tutto il contenuto iniziale e i componenti che possono essere utilizzati.

Con l’**Editor modelli**, la creazione e la manutenzione dei modelli non è più un’attività che riguarda solo gli sviluppatori. Può essere coinvolto anche un tipo di “power user”, detto **autore dimodelli**. Gli sviluppatori devono comunque occuparsi di configurare l’ambiente, creare le librerie client e i componenti da utilizzare, ma una volta che questi elementi di base sono implementati, l’**autore del modello** avrà la flessibilità di creare e configurare i modelli senza un progetto di sviluppo.

La **Console modelli** consente agli autori di modelli di:

* Creare un nuovo modello o copiarne uno esistente.
* Gestisci il ciclo di vita del modello.

L’**Editor modelli** consente agli autori di modelli di:

* Aggiungere i componenti al modello e posizionarli su una griglia dinamica.
* Preconfigurare i componenti.
* Definire quali componenti possono essere modificati nelle pagine create con il modello.

Questo documento illustra come un **autore di modelli** può utilizzare la console e l’editor modelli per creare e gestire modelli modificabili.

Per informazioni dettagliate su come funzionano i modelli modificabili a livello tecnico, consulta il documento per sviluppatori [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md) per ulteriori informazioni.

>[!NOTE]
>
>L’**Editor modelli** non supporta il targeting diretto a livello di modello. È possibile impostare come destinazione le pagine create in base a un modello modificabile, ma non i modelli stessi.

>[!CAUTION]
>
>Pagine e modelli creati con **Console modelli** non sono destinati all’utilizzo con l’interfaccia utente classica e tale utilizzo non è supportato.

## Prima di iniziare {#before-you-start}

>[!NOTE]
>
>Un amministratore deve configurare una cartella di modelli nel **browser delle configurazioni** e applicare le autorizzazioni appropriate prima che un autore possa creare un modello in tale cartella.

Prima di iniziare, è importante considerare i seguenti punti:

* La creazione di un nuovo modello richiede collaborazione. Per questo motivo per ogni attività è indicato il relativo [Ruolo.](#roles)

* A seconda della configurazione dell’istanza, potrebbe essere utile tenere presente che ora l’AEM fornisce [due tipi di modello di base](/help/sites-authoring/templates.md#editable-and-static-templates). Questo non influisce su come effettivamente [utilizzare un modello per creare una pagina](#using-a-template-to-create-a-page), ma influisce sul tipo di modello che è possibile creare e su come una pagina si relaziona al relativo modello.

### Ruoli {#roles}

La creazione di un nuovo modello tramite **Templates Console (Console modelli)** e **Editor modelli** richiede la collaborazione tra i seguenti ruoli:

* **Amministratore**:

   * Crea una nuova cartella per i modelli che richiede i diritti di `admin`.

   * Spesso tali attività possono essere eseguite anche da uno sviluppatore

* **Sviluppatore**:

   * Si concentra sui dettagli tecnici/interni
   * Deve avere esperienza con l’ambiente di sviluppo.
   * Fornisce all’autore del modello le informazioni necessarie.

* **Autore del modello**:

   * Questo è un autore specifico che è membro del gruppo `template-authors`

      * In questo modo vengono assegnati i privilegi e le autorizzazioni necessarie.

   * Può configurare l’utilizzo di componenti e di altri dettagli di alto livello che richiedono:

      * Alcune conoscenze tecniche

         * Ad esempio, l’utilizzo di pattern durante la definizione dei percorsi.

      * Informazioni tecniche fornite dallo sviluppatore.

A causa della natura di alcune attività, come la creazione di una cartella, è necessario un ambiente di sviluppo che richiede conoscenza/esperienza.

Le attività descritte nel presente documento sono elencate con il ruolo responsabile della loro esecuzione.

### Modelli modificabili e statici {#editable-and-static-templates}

L’AEM offre ora due tipi di modelli di base:

* [Modelli modificabili](/help/sites-authoring/templates.md#creatingandmanagingnewtemplates)

   * Può essere [creato](#creatinganewtemplate) e [modificato](#editingatemplate) dagli autori di modelli utilizzando **Modello** e l&#39;editor. Il **Modello** è accessibile nella **Generale** sezione del **Strumenti** console.

   * Dopo la creazione della nuova pagina, viene mantenuta una connessione dinamica tra la pagina e il modello. Ciò significa che le modifiche alla struttura del modello e/o al contenuto bloccato verranno applicate a tutte le pagine create con tale modello. Le modifiche al contenuto sbloccato (ovvero iniziale) non verranno applicate.
   * Utilizza i criteri per contenuto, che puoi definire dall’editor modelli, per mantenere le proprietà di progettazione. La modalità Progettazione nell’editor pagina non viene più utilizzata per i modelli modificabili.

* Modelli statici

   * Sono disponibili modelli statici per diverse versioni di AEM.
   * Sono [fornite dai tuoi sviluppatori](/help/sites-developing/page-templates-static.md), pertanto non possono essere create o modificate dagli autori.
   * Vengono copiate per creare la nuova pagina, ma non esiste alcuna connessione dinamica successiva (anche se il nome del modello è registrato per informazione).
   * Utilizzare [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md) per mantenere le proprietà di progettazione.
   * Poiché la modifica di modelli statici è un’attività esclusiva di uno sviluppatore, consulta il documento per gli sviluppatori [Modelli di pagina - Statici](/help/sites-developing/page-templates-static.md) per ulteriori informazioni.

Per definizione, la console dei modelli e l’editor dei modelli consentono solo la creazione e la modifica di modelli modificabili. Pertanto, questo documento si concentra esclusivamente sui modelli modificabili.

### Utilizzo di un modello per creare una pagina {#using-a-template-to-create-a-page}

Quando si utilizza un modello per [crea una nuova pagina](/help/sites-authoring/managing-pages.md#creating-a-new-page) non esiste alcuna differenza visibile né indicazione tra modelli statici e modificabili. Per l’autore della pagina, il processo è trasparente.

## Creazione e gestione di modelli {#creating-and-managing-templates}

Quando viene creato un nuovo modello modificabile:

* Utilizza la console dei **Modelli**. Questa funzione è disponibile nella sezione **Generale** della console degli **Strumenti**.

   * Oppure direttamente da: [https://localhost:4502/libs/wcm/core/content/sites/templates.html/conf](https://localhost:4502/libs/wcm/core/content/sites/templates.html/conf)

* Se necessario, puoi [creare una cartella per i modelli](#creating-a-template-folder-admin).
* [Crea un nuovo modello](#creatinganewtemplateauthor), che sarà inizialmente vuoto.

* Se necessario, [Definisci proprietà aggiuntive](#definingtemplatepropertiesauthor) per il modello
* [Modifica il modello](#editingtemplates) per definire:

   * [Struttura](#editingatemplatestructureauthor): contenuto predefinito che non può essere modificato nelle pagine create con il modello.
   * [Contenuto iniziale](#editing-a-template-initial-content-author): contenuto predefinito che potrà essere modificato nelle pagine create con il modello.
   * [Layout](#editingatemplatelayoutauthor): per una vasta gamma di dispositivi.
   * [Stili](/help/sites-authoring/style-system.md): definisci gli stili da utilizzare con il modello e i suoi componenti.

* [Abilita il modello](#enablingatemplateauthor) da utilizzare durante la creazione di una pagina
* [Consenti il modello](#allowing-a-template-author) per la pagina o la sezione richiesta del sito web
* [Pubblica il modello](#publishingatemplateauthor) per renderlo disponibile nell’ambiente di pubblicazione

>[!NOTE]
>
>I **Modelli consentiti** sono spesso predefiniti al momento della configurazione iniziale del sito web.

>[!CAUTION]
>
>Non inserire mai informazioni che devono essere [internazionalizzato](/help/sites-developing/i18n.md) in un modello. Ai fini dell&#39;internalizzazione, la [funzioni di localizzazione dei Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=it) sono consigliati.

### Creazione di una cartella di modelli - Amministratore {#creating-a-template-folder-admin}

È necessario creare una cartella di modelli per il progetto, che conterrà i modelli specifici per il progetto. Si tratta di un’attività amministrativa descritta nel documento [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md#template-folders).

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
   >I tipi di modello sono layout di modello predefiniti che possono essere considerati modelli di un modello. Sono predefiniti dagli sviluppatori o dall’amministratore di sistema. Per ulteriori informazioni consulta il documento per sviluppatori. [Modelli di pagina - Modificabili](/help/sites-developing/page-templates-editable.md#template-type).

1. Completa i **dettagli del Modello**:

   * **Nome modello**
   * **Descrizione**

1. Seleziona **Crea**. Viene visualizzata una conferma; seleziona **Apri**[](#editingatemplate) per iniziare a modificare il modello o **Fine** per tornare alla console dei modelli.

   >[!NOTE]
   >
   >Quando viene creato un nuovo modello, questo viene contrassegnato come **Bozza** nella console, a indicare che non è ancora disponibile per l’uso da parte degli autori di pagine.

### Definizione delle proprietà del modello - Autore del modello   {#defining-template-properties-template-author}

Un modello può avere le seguenti proprietà:

* Immagine

   * Immagine da utilizzare come [miniatura del modello](/help/sites-authoring/templates.md#template-thumbnail-image) per facilitare la selezione, ad esempio nella procedura guidata Crea pagina.

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
>I modelli sono strumenti potenti per semplificare il flusso di lavoro di creazione della pagina. Tuttavia, troppi modelli possono sopraffare gli autori e confondere la creazione di pagine. Una buona regola è mantenere il numero di modelli sotto i 100.
>
>Adobe consiglia di non disporre di più di 1000 modelli a causa di potenziali impatti sulle prestazioni.

>[!NOTE]
>
>Lo stato di un modello (bozza, attivato o disattivato) è indicato nella console.

#### Immagine della miniatura del modello {#template-thumbnail-image}

Per definire la miniatura del modello:

1. Modifica le proprietà del modello.
1. Scegli se desideri caricare una miniatura o generarla dal contenuto del modello.

   * Per caricare una miniatura, tocca o fai clic su **Carica immagine**
   * Per generare una miniatura, tocca o fai clic su **Genera anteprima**

1. Per entrambi i metodi viene visualizzata un’anteprima della miniatura.

   Se non ti soddisfa, tocca o fai clic su **Cancella** per caricare un’altra immagine o rigenerare la miniatura.

1. Quando la miniatura è soddisfacente, tocca o fai clic su **Salva e chiudi**.

### Abilitazione e autorizzazione di un modello - Autore del modello   {#enabling-and-allowing-a-template-template-author}

Per poter utilizzare un modello quando si crea una pagina, è necessario svolgere le seguenti operazioni:

* [Attiva i modelli](#enablingatemplate) per renderli disponibili per l’uso durante la creazione di pagine.
* [Consenti ai modelli](#allowingatemplate) di specificare i rami di contenuto in cui è possibile utilizzare il modello.

#### Abilitazione di un modello - Autore del modello {#enabling-a-template-template-author}

Un modello può essere abilitato o disabilitato per renderlo disponibile o non disponibile nella procedura guidata **Crea pagina**.

>[!CAUTION]
>
>Una volta abilitato un modello, viene visualizzato un avviso quando un autore inizia ad aggiornare ulteriormente il modello. In tal modo l’utente viene informato che è possibile fare riferimento al modello e che eventuali modifiche potrebbero interessare le pagine che vi fanno riferimento.

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

1. Sotto **Impostazioni modello** utilizzare **Aggiungi campo** per specificare i percorsi dei modelli.

   Il percorso può essere esplicito o utilizzare pattern. Esempio:

   `/conf/<your-folder>/settings/wcm/templates/.*`

   L’ordine dei percorsi è irrilevante, tutti i percorsi verranno analizzati e tutti i modelli recuperati.

   >[!NOTE]
   >
   >Se il **Modelli consentiti** L’elenco viene lasciato vuoto, quindi la struttura viene incrementata finché non viene trovato un valore o un elenco.
   >
   >
   >Consulta [Disponibilità dei modelli](/help/sites-developing/templates.md#template-availability): i principi per i modelli consentiti rimangono gli stessi.

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

Durante la creazione o la modifica di un modello è possibile definire vari aspetti. La modifica dei modelli è simile alla creazione delle pagine.

È possibile modificare i seguenti aspetti di un modello:

* [Struttura](#editingatemplatestructure)

  I componenti aggiunti in questo punto non possono essere spostati o rimossi dalle pagine risultanti dagli autori delle pagine. Se desideri permettere agli autori delle pagine di aggiungere e rimuovere componenti dalle pagine risultanti, è necessario aggiungere un sistema di paragrafi al modello.

  Quando i componenti sono bloccati, è possibile aggiungere contenuti che non possono essere modificati dagli autori delle pagine. Puoi sbloccare i componenti per definire [Contenuto iniziale](#editingatemplateinitialcontent).

  >[!NOTE]
  >
  >In modalità struttura, tutti i componenti che sono l’elemento principale di un componente sbloccato non possono essere spostati, tagliati o cancellati.

* [Contenuto iniziale](#editingatemplateinitialcontent)

  Quando un componente è stato sbloccato, è possibile definire il contenuto iniziale che verrà copiato nelle pagine risultanti, create dal modello. I componenti sbloccati possono essere modificati nella pagina o nelle pagine risultanti.

  >[!NOTE]
  >
  >Nella modalità **Contenuto iniziale** e nelle pagine risultanti, tutti i componenti sbloccati che hanno un elemento padre accessibile (ad esempio i componenti all’interno di un contenitore di layout) possono essere eliminati.

* [Layout](#editingatemplatelayout)

  Qui puoi predefinire il layout del modello per i formati di dispositivo richiesti. La modalità **Layout** per la creazione dei modelli ha le stesse funzionalità della modalità [**Layout** per la creazione delle pagine.](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)

* [Criteri di pagina](#editingatemplatepagepolicies)

  In Criteri di pagina è possibile collegare alla pagina i criteri di pagina predefiniti. I criteri di pagina definiscono le varie configurazioni di progettazione.

* [Stili](/help/sites-authoring/style-system.md)

  Il sistema di stili consente all’autore del modello di definire le classi di stile nel criterio del contenuto di un componente, in modo che un autore di contenuti possa sceglierli quando modifica un componente in una pagina. Gli stili possono essere varianti visive alternative di un componente, per renderlo più flessibile.

  Per ulteriori informazioni, consulta la [documentazione sul sistema di stili](/help/sites-authoring/style-system.md).

Il **Modalità** nella barra degli strumenti consente di selezionare e modificare l’aspetto appropriato del modello:

* [Struttura](#editingatemplatestructure)
* [Contenuto iniziale](#editingatemplateinitialcontent)
* [Layout](#editingatemplatelayout)

![chlimage_1-133](assets/chlimage_1-133.png)

Mentre il **Criterio pagina** opzione sul **Informazioni pagina** menu consente di: [seleziona i criteri di pagina richiesti](#editingatemplatepagepolicies):

![screen_shot_2018-03-23at120604](assets/screen_shot_2018-03-23at120604.png)

>[!CAUTION]
>
>Se un autore inizia a modificare un modello già abilitato, viene visualizzato un avviso. In tal modo l’utente viene informato che è possibile fare riferimento al modello e che eventuali modifiche potrebbero interessare le pagine che vi fanno riferimento.

### Modifica di un modello - Struttura - Autore del modello {#editing-a-template-structure-template-author}

In modalità **Struttura** si definiscono i componenti e i contenuti per il modello, nonché i criteri per il modello e i suoi componenti.

* I componenti definiti nella struttura del modello non possono essere spostati in una pagina risultante né eliminati dalle pagine risultanti.
* Se desideri che gli autori delle pagine possano aggiungere e rimuovere componenti, aggiungi un sistema di paragrafi al modello.
* I componenti possono essere sbloccati e bloccati di nuovo per consentirti di definire [contenuto iniziale](#editingatemplateinitialcontent).

* Vengono definiti i criteri di design per i componenti e la pagina.

![screen_shot_2018-03-23at120819](assets/screen_shot_2018-03-23at120819.png)

In entrata **Struttura** modalità dell’editor modelli:

* **Aggiungi componenti**

  Per aggiungere componenti al modello, esistono diversi meccanismi:

   * Dal browser **Componenti** nel pannello laterale.
   * Utilizzando il **Inserisci componente** opzione (**+** disponibile sulla barra degli strumenti dei componenti già presenti nel modello o nel **Trascina qui i componenti** casella.

   * Trascinando una risorsa (dal browser **Risorse** nel pannello laterale) direttamente sul modello per generare il componente appropriato in situ.

  Una volta aggiunto, ogni componente viene contrassegnato con:

   * Un bordo
   * Un marcatore per mostrare il tipo di componente
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

  Una volta aggiunti al modello, effettua le azioni sui componenti: Ogni singola istanza dispone di una barra degli strumenti che consente di accedere alle azioni disponibili; la barra degli strumenti dipende dal tipo di componente.

  ![screen_shot_2018-03-23at120909](assets/screen_shot_2018-03-23at120909.png)

  Può anche dipendere dalle azioni intraprese, ad esempio se un criterio è stato associato al componente, in tal caso l’icona di configurazione del progetto diventa disponibile.

* **Modifica e Configura**

  Con queste due azioni è possibile aggiungere contenuti ai componenti.

* **Bordo per indicare la struttura**

  Quando si lavora in modalità **Struttura**, un bordo arancione indica il componente attualmente selezionato. Una linea tratteggiata indica anche il componente principale.

  Ad esempio, nella schermata seguente **Testo** è selezionato, all&#39;interno di un **Contenitore di layout** (responsivegrid).

  ![chlimage_1-134](assets/chlimage_1-134.png)

* **Criteri e proprietà (generale)**

  I criteri relativi al contenuto (o alla progettazione) definiscono le proprietà di progettazione di un componente. Ad esempio, i componenti disponibili o le dimensioni minime/massime. Sono applicabili al modello (e alle pagine create con il modello).

  Crea un criterio per i contenuti o selezionane uno esistente per un componente. Questo consente di definire i dettagli della progettazione.

  ![chlimage_1-135](assets/chlimage_1-135.png) ![chlimage_1-136](assets/chlimage_1-136.png)

  La finestra di configurazione è divisa in due parti.

   * Nella parte sinistra, in **Criteri**, è possibile selezionare un criterio esistente.
   * Nella parte destra, in **Proprietà** è possibile impostare le proprietà specifiche del tipo di componente.

  Le proprietà disponibili dipendono dal componente selezionato. Ad esempio, per un componente testo le proprietà definiscono, tra le altre, le opzioni di copia e incolla, le opzioni di formattazione e lo stile di paragrafo.

  ***Criterio***

  I criteri relativi al contenuto (o alla progettazione) definiscono le proprietà di progettazione di un componente. Ad esempio, i componenti disponibili o le dimensioni minime/massime. Sono applicabili al modello (e alle pagine create con il modello).

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
  >Se vengono aggiunti come contenuto iniziale più componenti dello stesso tipo, lo stesso criterio si applica a tutti i componenti. Riflette la stessa restrizione in [**Modalità Progettazione** per modelli statici](/help/sites-authoring/default-components-designmode.md).

  ***Proprietà***

  Nell’intestazione **Proprietà** puoi definire le impostazioni del componente. L’intestazione presenta due schede:

   * Principale
   * Funzioni

  *Principale*

  Nella scheda **Principale** vengono definite le impostazioni più importanti del componente.

  Ad esempio, per un componente immagine le larghezze consentite possono essere definite insieme all’abilitazione del caricamento lento.

  Se per un’impostazione sono consentite più configurazioni, tocca o fai clic sul pulsante **Aggiungi** per aggiungerne un’altra.

  ![chlimage_1-141](assets/chlimage_1-141.png)

  Per rimuovere una configurazione, tocca o fai clic sul pulsante **Elimina** situato a destra della configurazione.

  Per rimuovere una configurazione, tocca o fai clic ** pulsante Elimina**.

  ![chlimage_1-142](assets/chlimage_1-142.png)

  *Funzioni*

  Il **Funzioni** Questa scheda ti consente di abilitare o disabilitare funzioni aggiuntive del componente.

  Ad esempio, per un componente immagine puoi definire le proporzioni di ritaglio, gli orientamenti consentiti per le immagini e se sono consentiti caricamenti.

  ![chlimage_1-143](assets/chlimage_1-143.png)

  >[!CAUTION]
  >
  >In AEM i rapporti di ritaglio sono definiti come **altezza/larghezza**. Questo differisce dalla definizione tradizionale di larghezza/altezza, per ragioni di compatibilità con versioni precedenti. Gli utenti che creano le pagine non noteranno alcuna differenza, purché sia stato definito chiaramente il **Nome**, che verrà visualizzato nell’interfaccia utente.

  >[!NOTE]
  >
  >[I criteri dei contenuti per i componenti che si avvalgono dell’editor Rich Text](/help/sites-administering/rich-text-editor.md#main-pars-header-206036638) possono essere definiti solo per le opzioni disponibili mediante tale editor tramite le impostazioni di interfaccia utente. [](/help/sites-administering/rich-text-editor.md#main-pars_header_206036638) [](/help/sites-administering/rich-text-editor.md#main-pars_header_206036638)

* **Criteri e proprietà (contenitore di layout)**

  Le impostazioni dei criteri e delle proprietà di un contenitore di layout sono simili a quelle di uso generale, ma con alcune differenze.

  >[!NOTE]
  >
  >La configurazione di un criterio è obbligatoria per i componenti contenitore in quanto consente di definire i componenti che saranno disponibili nel contenitore.

  La finestra di configurazione è divisa in due parti, come la finestra per uso generale.

  ***Criterio***

  I criteri relativi al contenuto (o alla progettazione) definiscono le proprietà di progettazione di un componente. Ad esempio, i componenti disponibili o le dimensioni minime/massime. Sono applicabili al modello (e alle pagine create con il modello).

  In **Criterio** puoi selezionare un criterio esistente da applicare al componente tramite il menu a discesa. Questo funziona come nell’uso generale della finestra.

  ***Proprietà***

  Nell’intestazione **Proprietà** è possibile scegliere quali componenti sono disponibili per il contenitore di layout e definirne le impostazioni. L’intestazione presenta tre schede:

   * Componenti consentiti
   * Componenti standard
   * Impostazioni reattive

  *Componenti consentiti*

  Nella scheda **Componenti consentiti**, puoi definire quali componenti sono disponibili per il contenitore di layout.

   * I componenti sono raggruppati in base ai rispettivi gruppi di componenti, che possono essere espansi e compressi.
   * È possibile selezionare un intero gruppo selezionando il nome del gruppo e deselezionando tutti gli elementi.
   * Il segno meno significa che è stato selezionato almeno un elemento del gruppo, ma non tutti.
   * È disponibile una ricerca per filtrare un componente in base al nome.
   * I numeri elencati a destra del nome del gruppo di componenti rappresentano il numero totale di componenti selezionati in tale gruppo indipendentemente dal filtro.

  ![chlimage_1-144](assets/chlimage_1-144.png)

  *Componenti standard*

  Nella scheda **Componenti predefiniti**, è possibile definire quali componenti vengono associati automaticamente a determinati tipi di file multimediali in modo che, quando un autore trascina una risorsa dal browser di risorse, AEM sappia a quale componente associarla. Per questa configurazione sono disponibili solo i componenti con aree di rilascio.

  Tocca o fai clic su **Aggiungi mappatura** per aggiungere un componente completamente nuovo e la mappatura del tipo MIME.

  Seleziona un componente nell’elenco e tocca o fai clic su **Aggiungi tipo** per aggiungere un altro tipo MIME a un componente già mappato. Fai clic sull’icona **Elimina** per rimuovere un tipo di MIME.

  ![chlimage_1-145](assets/chlimage_1-145.png)

  *Impostazioni reattive*

  Nella scheda **Impostazioni reattive** è possibile configurare il numero di colonne nella griglia risultante del contenitore layout.

* **Sblocca/Blocca componenti**

  È possibile sbloccare/bloccare i componenti per definire se il contenuto è disponibile per la modifica in modalità **Contenuto iniziale**.

  Quando un componente è stato sbloccato:

   * Nel bordo viene visualizzato un lucchetto aperto.
   * La barra degli strumenti del componente verrà regolata di conseguenza.
   * Tutti i contenuti già inseriti non saranno più visualizzati in modalità **Struttura**.

      * Il contenuto già inserito è considerato contenuto iniziale ed è visibile solo nella modalità **Contenuto iniziale**.

   * L’elemento padre di un componente sbloccato non può essere spostato, tagliato o cancellato.

  ![chlimage_1-146](assets/chlimage_1-146.png)

  Ciò include lo sblocco di componenti contenitore in modo che possano essere aggiunti altri componenti, sia in modalità **Contenuto iniziale** che sulle pagine risultanti. Se hai già aggiunto componenti/contenuti al contenitore prima di sbloccarlo, questi non saranno più visualizzati in modalità **Struttura** ma saranno presenti in modalità **Contenuto iniziale**. In **Modalità struttura**, verrà mostrato solo il componente del contenitore stesso con il suo elenco di **Componenti consentiti**.

  ![chlimage_1-147](assets/chlimage_1-147.png)

  Per risparmiare spazio, il contenitore layout non cresce per accogliere l’elenco dei componenti consentiti. Piuttosto, il contenitore diventa un elenco scorrevole.

  I componenti configurabili vengono visualizzati con l’icona **Policy**, che può essere toccata o su cui è possibile fare clic per modificare la policy e le proprietà del componente.

  ![chlimage_1-148](assets/chlimage_1-148.png)

* **Relazione con le pagine esistenti**

  Se la struttura viene aggiornata dopo la creazione di pagine basate sul modello, a tali pagine verranno applicate le modifiche apportate al modello. Questo fatto è segnalato da un avviso nella barra degli strumenti e da finestre di dialogo di conferma.

  ![chlimage_1-149](assets/chlimage_1-149.png)

### Modifica di un modello - Contenuto iniziale - Autore {#editing-a-template-initial-content-author}

La modalità **Contenuto iniziale** viene utilizzata per definire il contenuto che verrà visualizzato quando una pagina viene creata per la prima volta in base al modello. Il contenuto iniziale può quindi essere modificato da chi crea la pagina.

Sebbene tutto il contenuto creato in modalità **Struttura** sia visibile nel **Contenuto iniziale**, solo i componenti sbloccati possono essere selezionati e modificati.

>[!NOTE]
>
>La modalità **Contenuto iniziale** è in pratica una modalità di modifica per le pagine create con quel modello. Pertanto, i criteri non vengono definiti in modalità **Contenuto iniziale**, ma in [**modalità Struttura**](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

* I componenti sbloccati disponibili per la modifica sono contrassegnati. Quando sono selezionati, presentano un bordo blu:

  ![chlimage_1-150](assets/chlimage_1-150.png)

* I componenti sbloccati dispongono di una barra degli strumenti che consente di modificare e configurare il contenuto:

  ![chlimage_1-151](assets/chlimage_1-151.png)

* Se un componente del contenitore è stato sbloccato (in modalità **Struttura**), è possibile aggiungervi nuovi componenti (in modalità **Contenuto iniziale**). I componenti aggiunti in modalità **Contenuto iniziale** possono essere spostati o eliminati dalle pagine risultanti.

  È possibile aggiungere un componente utilizzando l’area **Trascina qui i componenti** o l’opzione **Inserisci nuovo componente** dalla barra degli strumenti del contenitore appropriato.

  ![chlimage_1-152](assets/chlimage_1-152.png) ![chlimage_1-153](assets/chlimage_1-153.png)

* Se il contenuto iniziale del modello viene aggiornato dopo la creazione delle pagine basate sul modello, tali pagine non saranno influenzate dalle modifiche apportate al contenuto iniziale del modello.

>[!NOTE]
>
>Il contenuto iniziale è destinato alla preparazione dei componenti e del layout di pagina, che fungono da punto di partenza per la creazione del contenuto. Non si tratta del contenuto effettivo, che rimarrebbe invariato. Per questo motivo, il contenuto iniziale non può essere tradotto.
>
>Per includere nel modello il testo traducibile, ad esempio nelle intestazioni o nei piè di pagina, puoi utilizzare le funzioni di [localizzazione dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=it).

### Modifica di un modello - Layout - Autore del modello {#editing-a-template-layout-template-author}

È possibile definire il layout del modello per una serie di dispositivi. Il [Layout reattivo](/help/sites-authoring/responsive-layout.md) per i modelli funziona come per la creazione delle pagine.

>[!NOTE]
>
>Le modifiche al layout verranno applicate in modalità **Contenuto iniziale**, ma non in modalità **Struttura**.

![chlimage_1-154](assets/chlimage_1-154.png)

### Modifica di un modello - Progettazione pagina - Autore/sviluppatore del modello {#editing-a-template-page-design-template-author-developer}

La progettazione della pagina, comprese le librerie lato client e le policy di pagina obbligatorie, viene mantenuta nell’opzione **Progettazione pagina** del menu **Informazioni pagina**.

Per accedere al **Progettazione pagina** finestra di dialogo:

1. Dalla sezione **Editor modelli**, seleziona **Informazioni pagina** dalla barra degli strumenti, quindi **Progettazione pagina** per aprire la finestra di dialogo.
1. Il **Progettazione pagina** viene visualizzata una finestra di dialogo divisa in due sezioni:

   * La metà a sinistra definisce i [criteri della pagina](/help/sites-authoring/templates.md#page-policies)
   * La metà a destra definisce le [proprietà della pagina](/help/sites-authoring/templates.md#page-properties)

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

#### Proprietà pagina {#page-properties}

Con le proprietà della pagina è possibile definire le librerie lato client richieste mediante la finestra di dialogo **Progettazione pagina**. Le librerie lato client includono fogli di stile e Javascript da caricare con il modello e le pagine create con tale modello.

![chlimage_1-162](assets/chlimage_1-162.png)

* Specifica le librerie lato client che desideri applicare alle pagine create con questo modello. Immetti il nome di una libreria nel campo di testo della sezione **Librerie lato client**.

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

1. Per confermare le definizioni, seleziona **Fine**.

## Best practice   {#best-practices}

Quando crei dei modelli, prendi in considerazione quanto segue:

1. L’impatto di eventuali modifiche apportate al modello dopo che sono state create delle pagine dal modello in questione.

   Di seguito è riportato un elenco delle diverse operazioni possibili sui modelli e di come influiscono sulle pagine create da essi:

   * Modifiche alla struttura:

      * Vengono applicate immediatamente alle pagine risultanti.
      * È comunque necessario pubblicare il modello modificato affinché i visitatori possano vedere le modifiche.

   * Modifiche ai criteri dei contenuti e alle configurazioni di progettazione:

      * Vengono applicate immediatamente alle pagine risultanti.
      * È necessario pubblicare le modifiche affinché i visitatori possano vederle.

   * Modifiche al contenuto iniziale:

      * Vengono applicate solo alle pagine create dopo la modifica del modello.

   * Le modifiche al layout dipendono dal ruolo del componente modificato:

      * Solo struttura: vengono applicate immediatamente
      * Con contenuto iniziale: vengono applicate immediatamente solo alle pagine create dopo la modifica

   Presta particolare attenzione nei seguenti casi:

   * Blocco o sblocco di componenti su modelli abilitati.
   * Questo può avere effetti secondari, in quanto le pagine esistenti possono già utilizzarlo. In genere:

      * Lo sblocco dei componenti (che erano bloccati) risulterà mancante nelle pagine esistenti.
      * I componenti bloccati (che erano modificabili) nascondono la visualizzazione di tale contenuto sulle pagine.

   >[!NOTE]
   >
   >AEM fornisce avvisi espliciti quando si modifica lo stato di blocco dei componenti nei modelli che non sono più bozze.

1. [Creazione di cartelle personalizzate](#creatingatemplatefolderdeveloper) per i modelli specifici del sito.
1. [Pubblica i modelli](#publishingatemplateauthor) dalla console **Modelli**.
