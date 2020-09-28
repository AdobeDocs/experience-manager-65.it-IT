---
title: Creazione e utilizzo di temi
seo-title: Creazione e utilizzo di temi
description: È possibile utilizzare i temi per stilizzare e fornire un'identità visiva a un modulo adattivo o a una comunicazione interattiva. È possibile condividere un tema tra un numero qualsiasi di moduli adattivi o comunicazioni interattive.
seo-description: È possibile utilizzare i temi per stilizzare e fornire un'identità visiva a un modulo adattivo o a una comunicazione interattiva. È possibile condividere un tema tra un numero qualsiasi di moduli adattivi o comunicazioni interattive.
uuid: 88b6b6fd-181b-48c5-ac15-2b37592bd14b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, interactive-communications
content-strategy: max-2018
discoiquuid: 770e9174-b648-462a-abe9-05fefa967d86
docset: aem65
translation-type: tm+mt
source-git-commit: d324586eb1d4fb809bf87641001b92a1941e6548
workflow-type: tm+mt
source-wordcount: '6062'
ht-degree: 1%

---


# Creazione e utilizzo di temi {#creating-and-using-themes}

## Introduzione {#introduction}

È possibile creare e applicare temi per stilizzare un modulo adattivo o una comunicazione interattiva. Un tema contiene dettagli di stile per i componenti e i pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori dello stato, la trasparenza, l’allineamento e le dimensioni. Quando si applica un tema, lo stile specificato si riflette sui componenti corrispondenti. I temi vengono gestiti in modo indipendente senza alcun riferimento a un modulo adattivo o a una comunicazione interattiva.

Operazioni disponibili:

* Creare un tema
* Modificare e copiare un tema esistente
* Scaricare e caricare un tema esistente  server AEM Forms
* Gestione delle dipendenze per un tema

## Creazione, download o caricamento di un tema {#creating-downloading-or-uploading-a-theme}

Con  AEM Forms potete creare, scaricare o caricare i temi. Un tema viene creato come altre risorse come moduli, documenti e lettere. Il tema viene salvato come entità separata, completa di meta-proprietà come i moduli. I temi, essendo un&#39;entità separata, possono essere riutilizzati in più moduli adattivi e nelle comunicazioni interattive. Potete anche spostare un tema in un’altra istanza di  AEM Forms e riutilizzarlo.

### Creazione di un tema {#creating-a-theme}

Per creare un tema, effettuate le seguenti operazioni:

1. Fate clic su **Adobe Experience Manager**, fate clic su **Forms**, quindi fate clic su **Temi**.

1. Nella pagina Temi, fate clic su **Crea > Tema**.
Viene avviata una procedura guidata per creare un tema.

1. Nella scheda Base della procedura guidata Crea tema, specificare **Titolo** e **Nome** del tema. Si tratta di campi obbligatori.

1. Nella scheda Avanzate sono disponibili due campi:

   * **Posizione** Clientlib: Posizione nella directory archivio in cui sono memorizzati i clientlibs per il tema.

   * **Categoria** Clientlib: Fornisce un campo di testo per immettere il nome della categoria clientlib per il tema.

1. Fate clic su **Crea** , quindi su **Modifica** per aprire il tema in Editor tema oppure fate clic su **Fine** per tornare alla pagina dei temi.

### Download di un tema {#downloading-a-theme}

Potete esportare i temi come file zip e usarli in altri progetti o AEM istanze. Per scaricare un tema:

1. Fate clic su **Adobe Experience Manager**, fate clic su **Forms**, quindi fate clic su **Temi**.

1. Nella pagina Temi, **selezionate** un tema e fate clic su **Scarica**. Viene visualizzata una finestra di dialogo con i dettagli del tema.

1. Fate clic su **Scarica**. Il tema viene scaricato come file zip.

>[!NOTE]
>
>Se scaricate un tema a cui è associato un modulo adattivo e il modulo adattivo associato si basa su un modello personalizzato, scaricate anche il modello personalizzato. Quando caricate il tema scaricato e il modulo adattivo su un server AEM Forms , caricate anche il modello personalizzato correlato.

### Caricamento di un tema {#uploading-a-theme}

Potete usare i temi creati con i predefiniti di stile del progetto. Potete importare pacchetti di temi creati da altri utenti caricandoli nel progetto.

Per caricare un tema:

1. Fate clic su **Adobe Experience Manager**, fate clic su **Forms**, quindi fate clic su **Temi**.

1. Nella pagina Temi, fate clic su **Crea > Caricamento** file.
1. Nel prompt Caricamento file, individuate e selezionate un pacchetto di temi sul computer e fate clic su **Carica**.
Il tema caricato è disponibile nella pagina dei temi.

## Metadati di un tema {#metadata-of-a-theme}

Elenco di meta-proprietà di un tema (trovato nella pagina delle proprietà di un tema).

<table>
 <tbody>
  <tr>
   <th><p><strong>ID</strong></p> <p> </p> </th>
   <th><strong>Nome</strong></th>
   <th><strong>Può essere modificato</strong></th>
   <th><strong>Descrizione proprietà</strong></th>
  </tr>
  <tr>
   <td>1.</td>
   <td>Titolo</td>
   <td>Sì</td>
   <td>Nome visualizzato del tema.</td>
  </tr>
  <tr>
   <td>2.</td>
   <td>Descrizione</td>
   <td>Sì</td>
   <td>Descrizione del tema.</td>
  </tr>
  <tr>
   <td>3.</td>
   <td>Tipo</td>
   <td>No</td>
   <td>
    <ul>
     <li>Tipo di risorsa.</li>
     <li>Il valore è sempre Tema.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>4.</td>
   <td>Creato</td>
   <td>No</td>
   <td>Data della creazione del tema</td>
  </tr>
  <tr>
   <td>5.</td>
   <td>Nome autore</td>
   <td>Sì</td>
   <td>Autore del tema. Calcolato al momento della creazione del tema.</td>
  </tr>
  <tr>
   <td>6.</td>
   <td>Data ultima modifica</td>
   <td>No</td>
   <td>Data dell’ultima modifica del tema.</td>
  </tr>
  <tr>
   <td>7.</td>
   <td>Stato</td>
   <td>No</td>
   <td>Stato del tema (Modificato/Pubblicato).</td>
  </tr>
  <tr>
   <td>8.</td>
   <td>Pubblica in base a tempo</td>
   <td>Sì</td>
   <td>Ora di pubblicare automaticamente il tema.</td>
  </tr>
  <tr>
   <td>9.</td>
   <td>Ora di disattivazione pubblicazione</td>
   <td>Sì</td>
   <td>Tempo per annullare automaticamente la pubblicazione del tema.</td>
  </tr>
  <tr>
   <td>10.</td>
   <td>Tag</td>
   <td>Sì</td>
   <td>Etichetta collegata al tema per l'identificazione utilizzata per migliorare la ricerca.</td>
  </tr>
  <tr>
   <td>11.</td>
   <td>Riferimenti</td>
   <td>Collegamenti</td>
   <td>
    <ul>
     <li>Contiene la sezione 'Referred by'. Elenca i moduli che utilizzano il tema.</li>
     <li>Poiché il tema non fa riferimento ad altre risorse, non è presente alcuna sezione 'Riferimenti'.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>12.</td>
   <td>Posizione Clientlib</td>
   <td>Sì</td>
   <td>
    <ul>
     <li>Percorso del repository definito dall'utente all'interno di '/etc' in cui sono memorizzati i clientlibs corrispondenti a questo tema.</li>
     <li>Valore predefinito - '/etc/clientlibs/fd/topics' + percorso relativo della risorsa tema.</li>
     <li>Se la posizione non esiste, la gerarchia delle cartelle viene generata automaticamente.</li>
     <li>Quando questo valore viene modificato, la struttura del nodo clientlib viene spostata nella nuova posizione immessa.<br /> <em><strong>Nota:</strong> Se si modifica il percorso clientlib predefinito, nell'archivio CRXDE assegnare <code>crx:replicate, rep:write, rep:glob:*, rep:itemNames:: js.txt, jcr:read </code>a <code>forms-users</code> e <code>crx:replicate</code>, <code>jcr:read </code>a <code>fd-service</code> nella nuova posizione. Aggiungi anche un altro ACL aggiungendo <code>deny jcr:addChildNodes</code> <code>forms-user</code></em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>13.</td>
   <td>Nome categoria Clientlib</td>
   <td>Sì</td>
   <td>
    <ul>
     <li>Il nome della categoria clientlib definita dall'utente per questo tema.</li>
     <li>Viene visualizzato un errore se il nome è già utilizzato da un altro tema esistente.</li>
     <li>Valore predefinito - calcolato utilizzando la posizione del tema.</li>
     <li>Quando questo valore viene modificato, il nome della categoria viene aggiornato sul nodo clientlib corrispondente. L'aggiornamento del nome della categoria Clientlib nei file jsp non è richiesto perché il nome della categoria clientlib è utilizzato dal riferimento.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Informazioni sull&#39;Editor tema {#about-the-theme-editor}

 AEM Forms viene fornito con Theme Editor. Si tratta di un&#39;interfaccia semplice per utenti aziendali e web-designer/sviluppatori che fornisce le funzionalità necessarie per specificare facilmente lo stile dei vari elementi di comunicazione interattiva e dei moduli adattivi. Quando si crea un tema, questo viene memorizzato come entità separata come moduli, comunicazioni interattive, lettere, frammenti di documento e dizionari di dati.

L’Editor tema consente di personalizzare gli stili dei componenti formattati in un tema. È possibile personalizzare l&#39;aspetto di un modulo o di una comunicazione interattiva su un dispositivo.

L’Editor tema è diviso in due pannelli:

* **Area di lavoro** - Visualizzata sul lato destro. Viene visualizzato un esempio di modulo adattivo o di comunicazione interattiva in cui tutte le modifiche dello stile vengono immediatamente applicate. È inoltre possibile selezionare gli oggetti direttamente dal quadro per cercare gli stili ad essi associati e per modificarli. Un righello di risoluzione del dispositivo nella parte superiore regola il quadro. Quando si seleziona un punto di interruzione della risoluzione dal righello, viene visualizzata l&#39;anteprima del modulo di esempio o la comunicazione interattiva per la relativa risoluzione. Il quadro è discusso in dettaglio [di seguito](../../forms/using/themes.md#using-canvas).

* **Barra laterale**- Visualizzata sul lato sinistro. Contiene i seguenti elementi:

   * **Selettore:** Mostra il componente selezionato per lo stile e le relative proprietà che è possibile definire. Il selettore rappresenta tutti i componenti di un tipo. Se si seleziona un componente casella di testo in un tema per la definizione dello stile, tutte le caselle di testo nel modulo o nella comunicazione interattiva erediteranno lo stile. I selettori consentono di selezionare un componente generico o un componente specifico per la definizione dello stile. Ad esempio, un componente Campo è un componente generico e una casella di testo è un componente specifico.

      **Attribuzione stile a un componente generico:**
Un campo può essere un campo casella numerica, ad esempio age o un campo casella di testo, ad esempio indirizzo.
Quando si formatta un campo, vengono formattati tutti i campi quali età, nome, indirizzo.

      **Attribuzione stile a un componente**specifico:
Un componente specifico interessa gli oggetti della categoria specifica. Quando si formatta il componente casella numerica nel tema, lo stile viene ereditato solo dall&#39;oggetto casella numerica.

      Ad esempio, un campo casella di testo come l&#39;indirizzo è più lungo in lunghezza e un campo casella numerico come l&#39;età è più corto in lunghezza. È possibile selezionare un campo casella numerica, ridurne la lunghezza e applicarlo al modulo. Nel modulo viene ridotta la larghezza di tutti i campi casella numerica.

      Quando personalizzate tutti i componenti campo con un colore di sfondo specifico, tutti i campi quali età, nome e indirizzo ereditano il colore di sfondo. Quando si seleziona una casella numerica, ad esempio age, e ne si riduce la larghezza, la larghezza di tutte le caselle numeriche, come l&#39;età, il numero di persone in una famiglia viene ridotto. La larghezza delle caselle di testo non viene modificata.

   * **Stato:** Consente di personalizzare gli stili di un oggetto in uno stato specifico. Ad esempio, è possibile specificare l&#39;aspetto di un oggetto quando è nello stato predefinito, attivo, disattivato, passaggio del mouse o di errore.
   * **Categorie di proprietà:** Le proprietà di stile sono suddivise in varie categorie. Dimension e posizione, testo, sfondo, bordo ed effetti. In ciascuna categoria vengono fornite informazioni sullo stile. Ad esempio, in Sfondo, potete fornire Colore di sfondo e Immagine e sfumatura.

   * **Avanzate:** Consente di aggiungere un CSS personalizzato a un oggetto, che sostituisce le proprietà definite dai controlli visivi in caso di sovrapposizione.

   * **Visualizza CSS**: Consente di visualizzare i CSS del componente selezionato
   Inoltre, nella barra laterale, in basso è presente una freccia. Quando fate clic sulla freccia, vengono visualizzate altre due opzioni: **Simulare il successo** e **simulare l&#39;errore.** Queste opzioni, insieme alle opzioni descritte sopra, sono discusse in dettaglio [di seguito](../../forms/using/themes.md#using-rail).

[ ![Editor di temi con Barra e Area di lavoro evidenziata.](assets/themes.png)](assets/themes-1.png) **A.** Barra laterale **B.** Canvas

### Styling components {#styling-components}

È possibile utilizzare un tema in più moduli adattivi e nelle comunicazioni interattive, per importare la formattazione del componente specificata nel tema. È possibile formattare vari componenti come titoli, descrizioni, pannelli, campi, icone e caselle di testo. Utilizzare i widget per configurare le proprietà dei componenti in un tema. La conoscenza precedente di CSS o LESS non è necessaria ma desiderata, anche se la sezione Ignorare i CSS consente di scrivere codice CSS o fornire selettori personalizzati. La sezione Sostituzioni CSS viene visualizzata quando selezionate un componente nella barra laterale.

![Componenti stilabili nella barra laterale](assets/stylable-components.png)

Opzioni nella barra laterale che consentono di selezionare e formattare diversi componenti.

Facendo clic sul pulsante Modifica rispetto a un componente nella barra laterale, il componente viene selezionato in Area di lavoro e potete definire lo stile del componente utilizzando le opzioni nella barra laterale.

Alcuni componenti come caselle di testo, caselle numeriche, pulsanti di scelta e caselle di controllo sono classificati in componenti generici come Campo. Ad esempio, è necessario personalizzare lo stile dei pulsanti di scelta. Per selezionare i pulsanti di scelta per lo stile, selezionare **Campo > Widget > Pulsante** di scelta.

Fate clic su **ESPANDI TUTTO** nella barra laterale per visualizzare, selezionare e formattare i componenti categorizzati che non sono visibili in primo piano.

### Layout del pannello Stile {#styling-panel-layouts-br}

I temi in  AEM Forms supportano lo stile degli elementi nel layout dei pannelli nei moduli e nelle comunicazioni interattive. È supportato lo stile degli elementi nei layout out-of-the-box e nei layout personalizzati.

I pannelli forniti includono:

* Schede a sinistra
* Schede in alto
* Pannello a soffietto
* Reattivo
* Wizard
* Layout mobile

   * Titoli del pannello nell’intestazione
   * Senza titoli del pannello nell’intestazione

I selettori variano a seconda del layout.
Lo stile di layout personalizzati dall&#39;Editor tema include:

* Definizione dei componenti per un layout che può essere formattato e selettori CSS per identificare in modo univoco questi componenti
* Definizione delle proprietà CSS che possono essere applicate a questi componenti
* Definire lo stile di questi componenti in modo interattivo dall’interfaccia utente

### Stili diversi per dimensioni di schermo diverse {#different-styles-for-different-screen-sizes-br}

I layout per desktop e dispositivi mobili possono avere stili leggermente diversi o completamente diversi. Per i dispositivi mobili, tablet e telefono condividono layout simili, tranne che per le dimensioni dei componenti.

Usate i punti di interruzione dell’Editor tema per definire lo stile alternativo per diverse dimensioni di schermo. Potete selezionare un dispositivo o una risoluzione di base su cui iniziare a creare il tema e le varianti di stile per altre risoluzioni vengono generate automaticamente. Potete modificare esplicitamente lo stile per tutte le risoluzioni.

>[!NOTE]
>
>Il tema viene creato innanzitutto utilizzando un modulo o una comunicazione interattiva, quindi applicato a moduli o comunicazioni interattive diversi. I punti di interruzione utilizzati nella creazione di un tema possono essere diversi dal modulo o dalla comunicazione interattiva su cui viene applicato il tema. Le query multimediali CSS si basano sul modulo o sulla comunicazione interattiva utilizzata per la creazione di temi e non sul modulo o sulla comunicazione interattiva a cui è applicato il tema.

### Modifica del contesto delle proprietà dello stile nella barra laterale durante la selezione degli oggetti {#styling-properties-context-changes-in-sidebar-on-selecting-objects}

Quando selezionate un componente nell’area di lavoro, le relative proprietà di stile sono elencate nella barra laterale. Selezionare il tipo di oggetto e il relativo stato, quindi specificarne lo stile.

### Stili usati di recente nell&#39;Editor tema {#recently-used-styles-in-theme-editor}

L’editor di temi memorizza nella cache fino a 10 stili applicati a un componente. Potete usare gli stili memorizzati nella cache con un altro componente di un tema. Gli stili utilizzati di recente sono disponibili sotto il componente selezionato nella barra laterale come casella di riepilogo. Inizialmente, l&#39;elenco degli stili utilizzati di recente è vuoto.

![asset-library](assets/asset-library.png)

Quando si formatta un componente, gli stili vengono memorizzati nella cache ed elencati nella casella di riepilogo. In questo esempio, l&#39;etichetta della casella di testo è formattata per modificare la dimensione e il colore del font. Per scegliere un’immagine o modificare i colori in base allo stile di un componente, potete seguire una procedura simile. Osservare come lo stile viene memorizzato nella cache ed elencato nella casella di riepilogo quando viene modificato lo stile dell&#39;etichetta del campo.

![Stile di font memorizzato nella cache per un componente disponibile per un altro](assets/font-style-cached.png)

In questo esempio, lo stile dell&#39;etichetta del campo viene modificato e quando si seleziona Descrizione pannello reattivo per lo stile, viene aggiunta una voce di elenco nella libreria delle risorse. La voce nella libreria delle risorse può essere utilizzata per modificare lo stile per Descrizione pannello reattivo.

Quando uno stile viene aggiunto nella libreria delle risorse, è disponibile per altri temi e nella modalità [di](../../forms/using/inline-style-adaptive-forms.md) stile dell’editor di moduli o dell’interfaccia utente dell’editor di comunicazioni interattivo. Allo stesso modo, quando si utilizza la modalità di stile dell’editor di moduli o dell’interfaccia utente dell’editor di comunicazioni interattive per formattare un componente, lo stile viene memorizzato nella cache ed è disponibile nei temi.

Il pulsante più (+) nella libreria delle risorse consente di salvare in modo permanente lo stile con il nome specificato. Il pulsante più salva lo stile anche se non si fa clic sul pulsante Salva nella barra laterale per applicare lo stile a un componente. Il pulsante più per salvare uno stile per un uso successivo non è disponibile in modalità stile.

![Specifica di un nome di stile personalizzato per la libreria di risorse](assets/custom-style-name.png)

Quando si fornisce un nome personalizzato per uno stile, lo stile è legato a un tema e non è più disponibile per altri temi. Per eliminare uno stile salvato:

1. Nella barra degli strumenti CANVAS, fate clic su Opzioni **tema (** Theme Options ![) Opzioni](assets/theme-options.png) **tema (tema) >** Gestisci stili(Manage Styles).
1. Nella finestra di dialogo Gestisci stili, selezionate uno stile salvato, fate clic su **Elimina**.

   ![Eliminare lo stile salvato](assets/manage-styles.png)

### Anteprima dal vivo, salvare ed eliminare le modifiche {#live-preview-save-and-discard-changes}

Le modifiche apportate allo stile vengono immediatamente riportate nel modulo o nella comunicazione interattiva caricata nell’area di lavoro. L&#39;anteprima dal vivo consente di definire e visualizzare in modo interattivo l&#39;impatto dello stile. Quando modificate lo stile di un componente, nella barra laterale viene attivato il pulsante **Fine** . Per mantenere le modifiche, fate clic sul pulsante **Fine** .

>[!NOTE]
>
>Quando si immette un carattere non valido in un campo, il colore del limite del campo diventa rosso e nell&#39;angolo superiore sinistro dello schermo viene visualizzato un messaggio di errore. Ad esempio, se si immettono alfabeti in una casella di testo che accetta caratteri numerici come input, il colore del limite della casella di input è cambiato in rosso. Non è possibile salvare un tema di questo tipo senza risolvere l&#39;errore visualizzato nella parte superiore.

### Tema con un altro modulo adattivo o comunicazione interattiva {#theme-with-another-adaptive-form-or-interactive-communication}

Quando si crea un tema, questo viene creato con un modulo fornito con l&#39;Editor tema. In questo modulo è disponibile lo stile per i componenti. Invece del modulo fornito con l&#39;Editor tema, è possibile selezionare un modulo o una comunicazione interattiva a scelta per fornire stile e visualizzare in anteprima i risultati.

Per sostituire il modulo corrente o la comunicazione interattiva nell&#39;area di lavoro dell&#39;Editor tema:

1. Nel pannello EDITOR TEMA, fate clic su Opzioni **tema (** Theme Options ![), opzioni](assets/theme-options.png) **tema (tema) >** Configura (Configure).

1. Nella scheda Generale, individuare e selezionare un modulo o una comunicazione interattiva per il campo Modulo/Documento **** adattivo.

### Ripristina/Annulla {#redo-undo}

Potete annullare o ripristinare le modifiche indesiderate che si verificano accidentalmente. Utilizzare i pulsanti Ripristina/Annulla nell’area di lavoro.

![Operazioni di ripristino e annullamento](assets/redo_undo_new.png)

Pulsanti Annulla/Ripristina nell’area di lavoro

I pulsanti Ripristina/Annulla vengono visualizzati quando si formatta un componente nell’Editor tema.

## Utilizzo dell&#39;Editor tema {#using-the-theme-editor}

L&#39;Editor tema consente di modificare un tema creato o caricato. Andate su **Forms e documenti > Temi**, selezionate un tema e apritelo. Il tema viene aperto nell’Editor tema.

Come già detto, l’Editor tema dispone di due pannelli: Barra laterale e quadro.
![editor di temi](assets/theme-editor.png)

Personalizzazione dello stile dello stato di successo del componente Widget casella di testo nell’Editor tema. Il componente è selezionato in Area di lavoro e il suo stato è selezionato nella barra laterale. Le opzioni di stile disponibili nella barra laterale consentono di personalizzare l’aspetto di un componente.

### Utilizzo del quadro {#using-canvas}

Il tema viene creato utilizzando il modulo out-of-the-box oppure utilizzando un modulo o una comunicazione interattiva a scelta dell&#39;utente. Il quadro mostra l&#39;anteprima del modulo o la comunicazione interattiva utilizzata per creare il tema con le personalizzazioni specificate nel tema. Il righello sopra il modulo viene utilizzato per determinare il layout in base alle dimensioni di visualizzazione del dispositivo.

Nella barra degli strumenti Area di lavoro sono disponibili le seguenti opzioni:

* **Attiva/disattiva pannello** laterale ![o pannello](assets/toggle-side-panel.png)laterale: Consente di mostrare o nascondere la barra laterale.
* **Opzioni** tema - ![opzioni](assets/theme-options.png)tema: Fornisce tre opzioni

   * Configura: Fornisce opzioni per selezionare il modulo di anteprima o la comunicazione interattiva, clientlib di base e  configurazione Adobe Fonts.
   * Visualizza CSS tema: Genera CSS per il tema selezionato.
   * Gestisci stili: Fornisce opzioni per gestire gli stili di testo e immagini
   * Aiuto: Esegue una visita guidata immagine dell&#39;Editor tema.

* **Emulatore** ![righello](assets/ruler.png): Emulazione dell’aspetto del tema per diverse dimensioni di visualizzazione. Una dimensione di visualizzazione viene trattata come un punto di interruzione nell&#39;emulatore. È possibile selezionare un punto di interruzione e specificarne uno stile. Ad esempio, Desktop e Tablet sono due punti di interruzione. È possibile specificare stili diversi per ciascun punto di interruzione.

Quando selezionate un componente nell’area di lavoro, compare sopra la barra degli strumenti del componente. La barra degli strumenti dei componenti consente di selezionare i componenti o di passare a componenti generici. Ad esempio, potete selezionare una casella di testo numerica in un pannello. Nella barra degli strumenti del componente sono disponibili le seguenti opzioni:

* **Widget** casella numerica: Consente di selezionare il componente per personalizzarne l’aspetto nella barra laterale.
* **Widget** campo: Consente di selezionare il componente generico da applicare allo stile. In questo esempio, tutti i componenti di immissione di testo (casella di testo/casella numerica/passo numerico/data di input) sono selezionati per lo stile.

* ![a livello](assets/field-level.png)di campo: Consente di passare a un componente generico per la definizione dello stile. Se si seleziona una casella numerica e si tocca questa icona, viene selezionato il componente Campo. Se selezionate il componente Campo e toccate questa icona, il pannello è selezionato. Toccando questa icona per la selezione, si finisce per selezionare il layout per lo stile.

>[!NOTE]
>
>Le opzioni disponibili nella barra degli strumenti del componente variano in base al componente selezionato.

![Barra degli strumenti del componente](assets/overlay.png)

Barra degli strumenti del componente nella casella numerica del quadro

### Utilizzo della barra laterale {#using-rail}

La barra laterale nell’editor di temi offre opzioni per personalizzare gli stili per i componenti di un tema e utilizzare i selettori. I selettori consentono di selezionare un gruppo di componenti o singoli componenti e di cercare i selettori nella barra laterale. È possibile scrivere selettori per componenti personalizzati.

Quando selezionate un componente dal quadro o dai selettori nella barra laterale, nella barra laterale vengono visualizzate tutte le opzioni che consentono di personalizzare gli stili per tale componente.
Di seguito sono riportate le opzioni visualizzate nella barra laterale quando si seleziona un componente:

* Stadio
* Foglio delle proprietà
* Simula errore/successo

#### Stadio {#state}

Uno stato è un indicatore dell’interazione dell’utente con un componente. Ad esempio, quando un utente immette dati errati in una casella di testo, lo stato della casella di testo diventa uno stato di errore. L’editor di temi consente di specificare lo stile per un particolare stato.

Le opzioni per la personalizzazione degli stili di stato variano per i diversi componenti.

#### Foglio delle proprietà {#property-sheet}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Utilizzo</strong></td>
  </tr>
  <tr>
   <td><p>Dimensioni e posizione</p> </td>
   <td><p>Consente di formattare l'allineamento, la dimensione, il posizionamento e il posizionamento dei componenti nel tema. </p> <p>Le opzioni disponibili sono l'impostazione di visualizzazione, la spaziatura, il margine, la larghezza, l'altezza e l'indice Z.</p> <p>È inoltre possibile utilizzare la modalità Layout per definire la larghezza dei componenti mediante una semplice interfaccia di trascinamento. Per ulteriori informazioni, vedere <a href="../../forms/using/resize-using-layout-mode.md">Uso della modalità Layout per ridimensionare i componenti</a>.</p> </td>
  </tr>
  <tr>
   <td><p>Testo</p> </td>
   <td><p>Consente di personalizzare gli stili di testo nel componente del tema.</p> <p>Ad esempio, è necessario modificare l'aspetto del testo immesso nella casella di testo.</p> <p>Le opzioni disponibili sono famiglia di font, spessore, colore, dimensione, altezza della riga, allineamento del testo, spaziatura tra lettere, rientro del testo, sottolineatura, corsivo, trasformazione del testo, allineamento verticale, linea di base e direzione. </p> </td>
  </tr>
  <tr>
   <td><p>Sfondo </p> </td>
   <td><p>Consente di riempire lo sfondo del componente con un’immagine o un colore. </p> </td>
  </tr>
  <tr>
   <td><p>Bordo</p> </td>
   <td><p>Consente di scegliere l’aspetto del bordo del componente. Ad esempio, si desidera che la casella di testo abbia un bordo rosso profondo e spesso con una linea punteggiata. </p> <p>Le opzioni disponibili sono larghezza, stile, raggio e colore del bordo.</p> </td>
  </tr>
  <tr>
   <td><p>Effetti</p> </td>
   <td><p>Consente di aggiungere effetti speciali ai componenti come opacità, metodo di fusione e ombre. </p> </td>
  </tr>
  <tr>
   <td><p>Avanzate </p> </td>
   <td><p>Consente di aggiungere:</p>
    <ul>
     <li>Proprietà per <code>::before</code> e <code>::after</code> pseudo elementi per aggiungere contenuto dopo o prima del contenuto predefinito nel selettore e formattarlo.<br /> Consultate Elementi Pseudo <a href="https://www.w3schools.com/css/css_pseudo_elements.asp" target="_blank">CSS</a>.</li>
     <li>Codice CSS personalizzato in linea con un componente e scrittura di selettori personalizzati. </li>
    </ul> <p>Quando aggiungete un codice CSS personalizzato, sostituisce la personalizzazione aggiunta utilizzando le opzioni nella barra laterale. </p> </td>
  </tr>
 </tbody>
</table>

#### Simula errore/successo {#simulate-error-success}

Le opzioni Simula errore e Successo sono disponibili nella parte inferiore della barra laterale. Potete visualizzarli utilizzando una freccia di tipo Mostra/Nascondi visibile nella parte inferiore della barra laterale. Utilizzando l&#39;Editor tema, è possibile formattare vari stati di un componente.

Ad esempio, è possibile aggiungere un campo numerico al modulo e specificarne lo stile nell&#39;editor di temi. Quando un utente digita un valore alfanumerico nel campo, occorre modificare il colore di sfondo della casella di testo. Selezionate il campo numerico nel tema e utilizzate l&#39;opzione di stato nella barra laterale. Selezionate lo stato Errore nella barra laterale e impostate il colore di sfondo su rosso. Per visualizzare l’anteprima del comportamento, potete utilizzare l’opzione Simula errore disponibile nella barra laterale. Le opzioni Simula errore e Successo sono descritte dettagliatamente di seguito:

* **Simula successo**:
Consente di visualizzare l’aspetto di un componente se ne specificate lo stile per il successo. Ad esempio, in un modulo i clienti impostano la password. Gli utenti possono impostare la password in base alle linee guida fornite. Quando un utente digita una password seguendo tutte le linee guida fornite, la casella di testo diventa verde. Quando la casella di testo diventa verde, lo stato è Successo. Potete specificare lo stile di un componente in stato di successo e simularne l’aspetto utilizzando l’opzione Simula esito positivo.

* **Simula errore**:
Consente di visualizzare l’aspetto di un componente se si specifica lo stile per lo stato di errore. Ad esempio, in un modulo i clienti impostano la password. Gli utenti possono impostare la password in base alle linee guida fornite. Quando un utente digita una password che non rispetta tutte le linee guida fornite, la casella di testo diventa rossa. Quando la casella di testo diventa rossa, si trova in stato di errore. Potete specificare lo stile di un componente in stato di errore e simularne l’aspetto utilizzando l’opzione Simula errore.

### Attribuzione dello stile a un componente {#styling-a-component}

Ad esempio, nel modulo sono disponibili due tipi di caselle di testo: che accetta solo valori numerici e altri che accettano valori alfanumerici. È possibile personalizzare lo stile della casella di testo che accetta solo valori numerici (una casella numerica).

Per personalizzare lo stile di un particolare componente, effettuate le seguenti operazioni (una casella numerica in questo esempio):

1. Nell&#39;Editor tema, selezionare la casella numerica nell&#39;area di lavoro.
1. Quando si seleziona la casella numerica, è possibile visualizzare la barra degli strumenti del componente con tre opzioni:

   * **Widget casella numerica**
   * **Widget** campo a livello di ![campo](assets/field-level.png)

1. Selezionare Widget **casella** numerica.
1. Il titolo della barra laterale diventa Widget Casella numerica e mostra le opzioni per personalizzarne l’aspetto.
Utilizzate l’opzione **Dimension e posizione** nella barra laterale per personalizzare le dimensioni del componente. Assicurarsi che lo stato sia **Predefinito**.

Anziché selezionare Widget **casella** numerica, selezionare Widget **** campo nella barra degli strumenti del componente ed eseguire la procedura descritta sopra. Quando si selezionano le dimensioni per l&#39;opzione Widget **** campo, tutte le caselle di testo tranne la casella numerica hanno la stessa dimensione.

### Attribuzione dello stile ai campi per un dato stato {#styling-fields-given-state}

Con la barra degli strumenti dei componenti, potete anche specificare lo stile dei componenti per i diversi stati. Ad esempio, se un componente è disabilitato, si trova in uno stato disabilitato. Gli stati usati comunemente di un componente che è possibile formattare nell’editor di temi sono: Predefinito, Attiva, Disattivato, Errore, Successo e Passaggio del mouse. Potete selezionare un componente nell’area di lavoro e utilizzare l’opzione Stato nella barra laterale per personalizzarne l’aspetto.

Per personalizzare lo stile di un componente in uno stato specifico, effettuate le seguenti operazioni:

1. Selezionate un componente nell’area di lavoro, quindi selezionate l’opzione appropriata dalla barra degli strumenti del componente.
La barra laterale mostra le opzioni per personalizzare lo stile del componente.
1. Selezionate uno stato nella barra laterale. Ad esempio, Stato errore.
1. Utilizzate opzioni quali **Bordo e Sfondo** nella barra laterale per personalizzare l’aspetto del componente.
1. Utilizzate l&#39;opzione **Simula errore** nella parte inferiore della barra laterale per vedere l&#39;aspetto dello stile nella modifica.

Quando personalizzate lo stile di un componente dopo averlo specificato, la personalizzazione viene visualizzata solo per il componente per lo stato specificato. Ad esempio, se personalizzate lo stile del componente quando è selezionato lo stato del passaggio del mouse. La personalizzazione viene visualizzata per il componente quando si passa il puntatore sul componente nel modulo di cui è stato effettuato il rendering o nella comunicazione interattiva a cui si applica il tema.

Per simulare il comportamento di stati diversi da errore e successo, utilizzate la modalità Anteprima. Per utilizzare la modalità Anteprima, fate clic su **Anteprima** nella barra degli strumenti della pagina.

### Layout di stile per schermi più piccoli {#styling-layouts-for-smaller-displays}

Utilizzate il righello in Area di lavoro per selezionare punti di interruzione per i dispositivi con display più piccoli. Fate clic sul ![righello](assets/ruler.png) emulatore nell’area di lavoro per visualizzare il righello e i punti di interruzione. I punti di interruzione consentono di visualizzare l&#39;anteprima di un modulo o di una comunicazione interattiva per le dimensioni di visualizzazione relative a dispositivi diversi, ad esempio telefoni e tablet. Nell&#39;Editor tema sono supportate più dimensioni di visualizzazione.

Per formattare i componenti per diversi punti di interruzione:

1. Nel quadro, selezionare un punto di interruzione sopra il righello.
Un punto di interruzione rappresenta un dispositivo mobile e le sue dimensioni di visualizzazione.
1. Utilizzate la barra laterale per personalizzare lo stile dei componenti di comunicazione modulo o interattiva nel tema per le dimensioni di visualizzazione selezionate.
1. Accertatevi che la personalizzazione sia salvata.

È possibile formattare moduli o componenti di comunicazione interattiva per più dispositivi. I componenti per moduli e comunicazioni interattive per desktop e dispositivi mobili possono avere stili completamente diversi.

### Utilizzo dei font Web in un tema {#using-web-fonts-in-a-theme}

È ora possibile utilizzare i font disponibili in un servizio Web in un modulo adattivo o in una comunicazione interattiva. Il servizio [Adobe Fonts](https://fonts.adobe.com/)è disponibile come configurazione  servizio di Adobe  font Web. Per utilizzare  Adobe Fonts, create un kit, aggiungete i font al suo interno e ottenete l&#39;ID kit da [Adobe Fonts](https://fonts.adobe.com/).

Effettuate le seguenti operazioni per configurare  Adobe Fonts in AEM:

1. Nell’istanza di authoring, fate clic su ![](assets/adobeexperiencemanager.png)adobeexperience emanagerExperience Manager  Adobe > ![martello](assets/hammer.png) Strumenti > Distribuzione > Cloud Services.
1. Nella pagina **Cloud Services** , individuate e aprite l’opzione **Adobe Fonts** . Aprite la cartella di configurazione e fate clic su **Crea**.
1. Nella finestra di dialogo **Crea configurazione** , specificate un titolo per la configurazione e fate clic su **Crea**.

   Viene nuovamente visualizzata la pagina di configurazione.

1. Nella finestra di dialogo Edit Component (Modifica componente) visualizzata, inserite l&#39;ID Kit e fate clic su **OK**.

Per configurare un tema in modo da utilizzare la configurazione Adobe Fonts , effettuate le seguenti operazioni:

1. Nell’istanza di creazione, aprite un tema nell’editor di temi.
1. Nell&#39;editor di temi, accedi a Opzioni **tema (** Theme Options) ![(Opzioni](assets/theme-options.png) tema) > **Configura (Configure)**.
1. Nel **campo Configurazione** Adobe Fonts, selezionate un kit e fate clic su **Salva**.

   Ora è possibile vedere i font aggiunti nella proprietà font-family del tema.

### Elenco e selezione dei font nell&#39;editor di temi {#listing-and-selecting-fonts-in-theme-editor}

Potete utilizzare il servizio di configurazione del tema per aggiungere altri font all&#39;editor del tema. Per aggiungere i font, effettuate le seguenti operazioni:

1. Accedi a AEM console Web con privilegi di amministratore. L&#39;URL per la console Web AEM è `https://'[server]:[port]'/system/console/configMgr`.
1. Aprire Il Servizio **Di Configurazione Tema Modulo** Adattivo.

   ![themoconfig](assets/theme-config.png)

1. Fate clic su +, specificate il nome del font e fate clic su **Salva**. Il font viene aggiunto e disponibile nell&#39;editor di temi.

#### Selezione dei font nell&#39;editor di temi {#selecting-fonts-in-theme-editor}

È possibile utilizzare il pulsante + per aggiungere un font. Quando aggiungete un font, questo viene elencato nella barra laterale.

![Nuovo font elencato nell&#39;editor di temi](assets/theme-font.png)

Oltre all&#39;opzione di configurazione del tema, potete anche aggiungere il font direttamente dall&#39;editor di temi. Digitare il font da utilizzare nel campo della famiglia di font sotto la barra laterale e premere il tasto Invio sulla tastiera.

![Digitare e selezionare il font nell&#39;editor di temi](assets/font-selection.png)

Quando si seleziona un font, questo viene aggiunto nell&#39;elenco della famiglia di font. Potete utilizzare l&#39;opzione Maschera nell&#39;editor di temi per disattivare o abilitare i font elencati.

![font multipli](assets/multi-fonts.jpg)

È possibile visualizzare la modifica del font del componente.

Il campo Famiglia font supporta più font. Quando digitate un font, il browser lo cerca e lo applica al componente selezionato. Se il browser non riesce a trovare un font, cerca il font accanto ad esso nella famiglia. È possibile iniziare digitando il font specifico che si sta cercando. Se non si trova il font che si desidera utilizzare, è possibile digitare un font generico nella famiglia e utilizzarlo.

#### Stili di maschera applicati nell&#39;editor di temi {#mask-styles-applied-in-theme-editor}

Potete applicare una maschera agli stili applicati a un tema. Nella barra laterale dell’editor di temi, potete usare l’icona ![toggle_](assets/toggle_eye.png)eyeicon per disattivare uno stile applicato. Ad esempio, se modificate le dimensioni di un componente in un modulo o in una comunicazione interattiva, potete utilizzare il pulsante maschera a sinistra di una proprietà per disattivarlo. Quando salvate un tema, le opzioni di mascheratura selezionate vengono mantenute.

![Opzione Maschera disponibile nella barra laterale dell’editor di temi](assets/mask-styles.png)

L&#39;esempio seguente mostra gli stili mascherati e non mascherati in un tema.

![Stili mascherati e non mascherati](assets/mask2.png)

## Applicazione di un tema a un modulo o a una comunicazione interattiva {#applying-a-theme-to-a-form-or-interactive-communication-br}

Per applicare un tema a un modulo adattivo:

1. Aprire il modulo in modalità di modifica. Per aprire un modulo in modalità di modifica, selezionare un modulo e fare clic su **Apri**.
1. In modalità di modifica, selezionare un componente, fare clic su ![campo](assets/field-level.png) > Contenitore **modulo** adattivo, quindi fare clic su ![cmppr](assets/cmppr.png).

   È possibile modificare le proprietà del modulo nella barra laterale.

1. Nella barra laterale, fate clic su **Attribuzione stile**.
1. Selezionate il tema dal menu a discesa Tema **modulo** adattivo e fate clic sul pulsante **Fine** ![controllo](assets/check-button.png).

Per applicare un tema a una comunicazione interattiva:

1. Aprite la comunicazione interattiva in modalità di modifica. Per aprire una comunicazione interattiva in modalità di modifica, selezionare un modulo e fare clic su **Apri**.
1. In modalità di modifica, selezionate un componente, fate clic su livello ![di](assets/field-level.png) campo > Contenitore **** documento, quindi fate clic su ![cmppr](assets/cmppr.png).

   È possibile modificare le proprietà del modulo nella barra laterale.

1. Nella barra laterale, in **Base**, selezionate il tema dal menu a discesa **Tema** e fate clic sul pulsante **Fine** ![controllo](assets/check-button.png)

### Modifica del tema di un modulo in fase di esecuzione {#change-theme-of-a-form-at-runtime}

Un tema stili diversi componenti di un modulo. È possibile utilizzare la `themeOverride` proprietà per modificare dinamicamente il tema di un modulo. Un tipico URL di un modulo è:

`https://<server>:<port>/content/forms/af/test.html`

Potete utilizzare il parametro temaOverride per applicare un tema al runtime.

`https://<server>:<port>/content/forms/af/test.html?themeOverride=/content/dam/formsanddocuments-themes/simpleEnrollmentTheme`

L&#39; `themeOverride` opzione consente di fornire un percorso a un tema. Cambia il tema del modulo e aggiorna il modulo con gli stili aggiornati.

## Ottenimento di un aspetto specifico tramite Temi {#specific-af-appearance}

Con  AEM Forms, insieme a un tema quadro predefinito, ci sono molti altri temi. Se si desidera progettare il modulo o la comunicazione interattiva utilizzando altri temi, insieme ad altre modifiche, copiare il tema dalla cartella Libreria temi. Incollate i temi copiati all’esterno della cartella Libreria temi e modificate il tema copiato in base alle modifiche desiderate.

Per copiare un tema, effettuate le seguenti operazioni:

1. Nell’istanza di creazione, passa a **Adobe Experience Manager > Forms > Temi**.
1. Aprite la cartella Libreria temi.
1. Nella cartella Libreria temi, passate il puntatore del mouse sul tema out-of-the-box corrispondente e toccate **Copia**.
1. Incollate il tema copiato fuori dalla cartella Libreria temi.
1. Personalizzare il tema copiato.

Dopo aver personalizzato il tema, applicatelo al modulo o alla comunicazione interattiva.

>[!NOTE]
>
>Non modificate i temi disponibili nella cartella Libreria temi. Questa cartella contiene i temi del sistema. Eventuali modifiche apportate a questi temi vengono sovrascritte al momento dell’installazione di una versione più recente o  correzione rapida di AEM Forms.

## Impatto su altri casi di utilizzo di moduli adattivi {#impact-on-other-adaptive-form-use-cases}

* **Pubblicare/annullare la pubblicazione di un modulo:** Quando si pubblica un modulo, viene pubblicato anche il tema a cui è stato applicato (se non è già pubblicato)
* **Importare/esportare un modulo:** Durante l&#39;importazione o l&#39;esportazione di un modulo, anche il tema associato viene importato o esportato automaticamente.
* **Riferimenti a un modulo:** La sezione Riferimenti nei riferimenti del modulo contiene una voce aggiuntiva per il tema.
* **Ora ultima modifica di un modulo:** Aggiornato quando il tema associato viene modificato.
* **Test A/B:** È possibile applicare un tema diverso a due versioni del modulo nel test A/B. Le informazioni dei due temi sono memorizzate singolarmente nei due contenitori di guida.

## Sequenza di generazione CSS {#css-generation-sequence}

Quando selezionate Visualizza CSS, Editor tema raccoglie tutte le informazioni sullo stile e crea un CSS. Raccoglie le informazioni nel seguente ordine:

1. Stile definito nella libreria client di base del tema.
1. Stile definito dall’utente, specificato utilizzando le proprietà nella barra laterale.
1. Stile CSS fornito utilizzando l&#39;opzione Override CSS.

Ad esempio, il colore di sfondo di una casella di testo è blu nella libreria client di base. Potete modificarlo in rosa utilizzando le proprietà nella barra laterale. Quando generate i CSS, il colore di sfondo della casella di testo viene visualizzato in rosa. Dopo aver modificato il colore di sfondo utilizzando le proprietà, un altro autore utilizza l&#39;opzione di sostituzione CSS per modificare la casella di testo del colore di sfondo come bianca. Quando generate i CSS, il colore di sfondo viene visualizzato come bianco nel CSS generato.

## Debug degli stili {#debugging-styles}

Quando specificate gli stili per i componenti in Editor tema, viene generato un CSS. Quando si formatta un componente generico, vengono formattati anche più componenti inclusi in esso. Ad esempio, quando si formatta un campo, anche la casella di testo e l’etichetta al suo interno sono formattate. Quando si formatta la casella di testo all&#39;interno del campo, viene creato un CSS personalizzato. Se si desidera eseguire il debug del CSS generato per il campo e il componente, l&#39;Editor tema fornisce opzioni che consentono di visualizzare i CSS.

Potete visualizzare i CSS generati utilizzando le seguenti opzioni:

* **Opzione Visualizza CSS** nella barra laterale: Quando selezionate un componente nel tema, potete visualizzare l’opzione VISUALIZZA CSS nella barra laterale. Mostra il CSS generato, inclusi i CSS per `::before` e gli `::after` pseudo elementi.
* **Opzione Visualizza CSS** tema nella barra degli strumenti canvas: Nella barra degli strumenti quadro, fate clic su ![tema-opzioni](assets/theme-options.png) > **Visualizza CSS** tema. Potete visualizzare l&#39;intero CSS del tema generato dalle proprietà definite nell&#39;Editor tema.

## Risoluzione di problemi, raccomandazioni e best practice {#troubleshooting-recommendations-and-best-practices}

* **Evitare la presenza di risorse da un altro tema**

   Quando modificate un tema, potete sfogliare e aggiungere risorse (come le immagini) da altri temi. Ad esempio, si sta modificando lo sfondo di una pagina. Ad esempio, quando si seleziona **Pagina** , ![Modifica pulsante](assets/edit-button.png)> **Sfondo** > **Aggiungi** > **Immagine**, viene visualizzata una finestra di dialogo che consente di sfogliare e aggiungere immagini in altri temi.

* Potete affrontare problemi con il tema corrente se una risorsa viene aggiunta da un altro tema e l’altro tema viene spostato o eliminato. È consigliabile evitare di sfogliare e aggiungere risorse da altri temi.
* **Utilizzo di clientlib di base, editor di temi e stile in linea**

   * **clientlib** di base:

      La libreria client di base contiene informazioni sullo stile. Per utilizzare le informazioni sullo stile nelle librerie lato client nei temi.

      1. Andate a **Experience Manager > Forms > Temi**.
      1. Nella pagina Temi, selezionate un tema e fate clic su **Visualizza proprietà**.
      1. Nella pagina Proprietà visualizzata, fate clic su **Avanzate**.
      1. Nella scheda Avanzate, nel campo Posizione Clientlib, individuare e selezionare la libreria client da utilizzare.
      1. Fai clic su **Salva**.

      Lo stile specificato nella libreria client viene importato nel tema che lo utilizza. Ad esempio, potete specificare lo stile per le caselle di testo, le caselle numeriche e il passaggio alla libreria client. Quando importate la libreria client nel tema, viene importato lo stile per le caselle di testo, le caselle numeriche e il pulsante. Potete quindi creare degli stili per altri componenti utilizzando l&#39;editor di temi.
Potete anche creare un tema, crearne delle copie e quindi modificare lo stile fornito nei temi copiati per casi di utilizzo simili.
Consultate [Ottenimento di un aspetto specifico con i temi](#specific-af-appearance)

   * **Editor temi:**

      L&#39;Editor tema consente di creare i temi per definire lo stile del modulo o della comunicazione interattiva. È possibile specificare lo stile dei componenti in un tema, che consente coerenza nell&#39;aspetto e nel comportamento tra più moduli o comunicazioni interattive sviluppate. È consigliabile specificare le informazioni sullo stile in un tema e quindi applicare il tema a un modulo.

   * **Stile in linea:**

      Quando si lavora con un modulo, è possibile formattare i componenti utilizzando la modalità Stile nell&#39;editor multicanale di comunicazione interattiva o modulo. Se si utilizza la modalità stile per modificare lo stile del componente modulo, lo stile specificato nel tema viene ignorato. Per modificare lo stile di alcuni componenti di un particolare modulo, vedere [Stile in linea dei componenti](../../forms/using/inline-style-adaptive-forms.md).


* **Utilizzo di librerie lato client**

   Se desiderate creare librerie client per importare informazioni sullo stile, consultate [Utilizzo delle librerie](/help/sites-developing/clientlibs.md)lato client. Dopo aver creato una libreria client, potete importarla nel tema utilizzando i passaggi indicati sopra.

* **Modifica della larghezza del layout del pannello contenitore**

   Non è consigliabile modificare la larghezza del layout del pannello contenitore. Quando specificate la larghezza di un pannello contenitore, questo diventa statico e non si adatta a diversi schermi.

* **Quando utilizzare l&#39;editor di moduli o temi per lavorare con intestazione e piè di pagina**

   Usate l’editor di temi per formattare intestazione e piè di pagina utilizzando opzioni di stile quali stile del font, sfondo e trasparenza.
Per fornire informazioni quali un&#39;immagine logo, il nome della società nell&#39;intestazione e le informazioni sul copyright nel piè di pagina, utilizzare le opzioni dell&#39;editor moduli.
