---
title: Creazione e utilizzo di temi
description: Puoi utilizzare i temi per applicare uno stile e fornire un’identità visiva a un modulo adattivo o a una comunicazione interattiva. Puoi condividere un tema in qualsiasi numero di moduli adattivi o comunicazioni interattive.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, interactive-communications
content-strategy: max-2018
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 93c360a8-a9d9-4c4b-b7e2-2c44eaf4604c
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '6084'
ht-degree: 1%

---

# Creazione e utilizzo di temi {#creating-and-using-themes}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/themes.html?lang=it) |
| AEM 6.5 | Questo articolo |

## Introduzione {#introduction}

Puoi creare e applicare temi per formattare un modulo adattivo o una comunicazione interattiva. Un tema contiene dettagli sullo stile dei componenti e dei pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l’allineamento e le dimensioni. Quando applicate un tema, lo stile specificato viene riflesso sui componenti corrispondenti. I temi sono gestiti in modo indipendente senza fare riferimento a un modulo adattivo o a una comunicazione interattiva.

Operazioni disponibili:

* Creare un tema
* Modificare e copiare un tema esistente
* Scarica e carica un tema esistente sul server AEM Forms
* Gestire le dipendenze per un tema

## Creazione, download o caricamento di un tema {#creating-downloading-or-uploading-a-theme}

Con AEM Forms puoi creare, scaricare o caricare temi. Un tema viene creato come altre risorse, ad esempio moduli, documenti e lettere. Il tema viene salvato come entità separata, completa di metaproprietà come i moduli. I temi sono un’entità separata e possono essere riutilizzati in più moduli adattivi e comunicazioni interattive. Puoi anche spostare un tema in un’istanza diversa di AEM Forms e riutilizzarlo.

### Creazione di un tema {#creating-a-theme}

Per creare un tema, effettua le seguenti operazioni:

1. Clic **Adobe Experience Manager**, fai clic su **Forms** e quindi fare clic su **Temi**.

1. Nella pagina Temi fare clic su **Crea > Tema**.
Viene avviata una procedura guidata per creare un tema.

1. Nella scheda Base della procedura guidata Crea tema, fornisci **Titolo** e **Nome** del tema. Si tratta di campi obbligatori.

1. Nella scheda Avanzate sono disponibili due campi:

   * **Posizione Clientlib**: posizione nell’archivio in cui sono memorizzate le clientlibs per il tema.

   * **Categoria Clientlib**: fornisce un campo di testo per immettere il nome della categoria clientlib per il tema.

1. Clic **Crea** e quindi fare clic su **Modifica** per aprire il tema nell’Editor tema, oppure fai clic su **Fine** per tornare alla pagina dei temi.

### Download di un tema {#downloading-a-theme}

Puoi esportare i temi come file zip e utilizzarli in altri progetti o istanze AEM. Per scaricare un tema:

1. Clic **Adobe Experience Manager**, fai clic su **Forms** e quindi fare clic su **Temi**.

1. Nella pagina Temi, **Seleziona** un tema e fai clic su **Scarica**. Viene visualizzata una finestra di dialogo con i dettagli del tema.

1. Clic **Scarica**. Il tema viene scaricato come file zip.

>[!NOTE]
>
>Se scarichi un tema a cui è associato un modulo adattivo e il modulo adattivo associato è basato su un modello personalizzato, scarica anche il modello personalizzato. Quando carichi il tema scaricato e il modulo adattivo su un server AEM Forms, carica anche il modello personalizzato correlato.

### Caricamento di un tema {#uploading-a-theme}

Puoi utilizzare i temi creati con predefiniti di stile sul progetto. Puoi importare pacchetti tema creati da altri caricandoli sul progetto.

Per caricare un tema:

1. Clic **Adobe Experience Manager**, fai clic su **Forms** e quindi fare clic su **Temi**.

1. Nella pagina Temi fare clic su **Crea > Caricamento file**.
1. Nella richiesta di caricamento file, individua e seleziona un pacchetto di temi sul computer e fai clic su **Carica**.
Il tema caricato è disponibile nella pagina dei temi.

## Metadati di un tema {#metadata-of-a-theme}

Elenco delle metaproprietà di un tema (disponibili nella pagina delle proprietà di un tema).

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
     <li>Il valore è sempre un tema.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>4.</td>
   <td>Creato</td>
   <td>No</td>
   <td>Data di creazione del tema</td>
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
   <td>Stato del tema (modificato/pubblicato).</td>
  </tr>
  <tr>
   <td>8.</td>
   <td>Ora di pubblicazione</td>
   <td>Sì</td>
   <td>Tempo per pubblicare automaticamente il tema.</td>
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
   <td>Etichetta associata al tema per l’identificazione utilizzata per migliorare la ricerca.</td>
  </tr>
  <tr>
   <td>11</td>
   <td>Riferimenti</td>
   <td>Collegamenti</td>
   <td>
    <ul>
     <li>Contiene la sezione "Referrer by". Elenca i moduli che utilizzano il tema.</li>
     <li>Poiché il tema non fa riferimento a nessun’altra risorsa, non è disponibile la sezione "Riferimenti".</li>
    </ul> </td>
  </tr>
  <tr>
   <td>12</td>
   <td>Posizione Clientlib</td>
   <td>Sì</td>
   <td>
    <ul>
     <li>Percorso dell’archivio definito dall’utente all’interno di "/etc" in cui sono memorizzate le clientlibs corrispondenti a questo tema.</li>
     <li>Valore predefinito - "/etc/clientlibs/fd/theme" + percorso relativo della risorsa tema.</li>
     <li>Se la posizione non esiste, la gerarchia di cartelle viene generata automaticamente.</li>
     <li>Quando questo valore viene modificato, la struttura del nodo clientlib viene spostata nella nuova posizione immessa.<br /> <em><strong>Nota:</strong> Se modifichi la posizione predefinita della libreria client, nell’archivio CRXDE assegna <code>crx:replicate</code>, <code>rep:write</code>, <code>rep:glob:*</code>, <code>rep:itemNames::</code> <code>js.txt</code>, <code>jcr:read</code> a <code>forms-users</code> e <code>crx:replicate</code>, <code>jcr:read</code> a <code>fd-service</code> nella nuova posizione. Allega un altro ACL aggiungendo <code>deny jcr:addChildNodes</code> per <code>forms-user</code></em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>13</td>
   <td>Nome categoria Clientlib</td>
   <td>Sì</td>
   <td>
    <ul>
     <li>Nome della categoria clientlib definita dall'utente per questo tema.</li>
     <li>Viene visualizzato un errore se il nome è già utilizzato da un altro tema esistente.</li>
     <li>Valore predefinito: calcolato utilizzando la posizione del tema.</li>
     <li>Quando questo valore viene modificato, il nome della categoria viene aggiornato sul nodo clientlib corrispondente. L’aggiornamento del nome della categoria Clientlib nei file jsp non è necessario perché il nome della categoria clientlib viene utilizzato come riferimento.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Informazioni sull’Editor tema {#about-the-theme-editor}

AEM Forms viene fornito con l’Editor temi. Si tratta di un’interfaccia intuitiva per utenti aziendali e web designer/sviluppatori che offre le funzionalità necessarie per specificare facilmente lo stile di vari elementi di comunicazione interattivi e moduli adattivi. Quando si crea un tema, questo viene memorizzato come entità separata, ad esempio moduli, comunicazioni interattive, lettere, frammenti di documento e dizionari dati.

L’Editor tema consente di personalizzare gli stili dei componenti a cui è applicato uno stile in un tema. È possibile personalizzare l&#39;aspetto di un modulo o di una comunicazione interattiva su un dispositivo.

L’Editor tema è suddiviso in due pannelli:

* **Area di lavoro** - Appare sul lato destro. Mostra un modulo adattivo di esempio o una comunicazione interattiva in cui tutte le modifiche di stile si riflettono immediatamente. È inoltre possibile selezionare gli oggetti direttamente dall&#39;area di lavoro per cercare gli stili ad essi associati e modificarli. L’area di lavoro è gestita da un righello di risoluzione dispositivo posto nella parte superiore. Selezionando un punto di interruzione di risoluzione dal righello viene visualizzata l&#39;anteprima del modulo di esempio o della comunicazione interattiva per la rispettiva risoluzione. L’area di lavoro viene discussa in dettaglio [sotto](../../forms/using/themes.md#using-canvas).

* **Barra laterale**- Appare sul lato sinistro. Include i seguenti elementi:

   * **Selettore:** Mostra il componente selezionato per lo stile e le relative proprietà che è possibile applicare allo stile. Il selettore rappresenta tutti i componenti di un tipo. Se si seleziona un componente casella di testo in un tema per lo stile, lo stile verrà ereditato da tutte le caselle di testo del modulo o dalla comunicazione interattiva. I selettori consentono di selezionare un componente generico o un componente specifico per lo stile. Ad esempio, un componente campo è un componente generico e una casella di testo è un componente specifico.

     **Componente generico di stile:**
Un campo può essere un campo casella numerica, ad esempio età, oppure un campo casella di testo, ad esempio indirizzo.
Quando si applica uno stile a un campo, lo stile viene applicato a tutti i campi, ad esempio età, nome e indirizzo.

     **Componente specifico per lo stile**: un componente specifico influisce sugli oggetti della categoria specifica. Quando si applica uno stile al componente casella numerica nel tema, solo l&#39;oggetto casella numerica in eredita lo stile.

     Ad esempio, un campo casella di testo come l&#39;indirizzo ha una lunghezza maggiore e un campo casella numerica come l&#39;età ha una lunghezza inferiore. È possibile selezionare un campo casella numerica, ridurne la lunghezza e applicarlo al modulo. La larghezza di tutti i campi casella numerica viene ridotta nel modulo.

     Quando personalizzi tutti i componenti campo con un colore di sfondo specifico, tutti i campi come età, nome e indirizzo ereditano il colore di sfondo. Quando si seleziona una casella numerica, ad esempio età, e se ne riduce la larghezza, la larghezza di tutte le caselle numeriche, ad esempio età, viene ridotto il numero di persone in una famiglia. La larghezza delle caselle di testo non viene modificata.

   * **Stato:** Consente di personalizzare gli stili di un oggetto in uno stato specifico. È ad esempio possibile specificare l&#39;aspetto di un oggetto quando si trova nello stato predefinito, attivo, disattivato, al passaggio del mouse o di errore.
   * **Categorie di proprietà:** Le proprietà di stile sono suddivise in varie categorie. Dimension e posizione, testo, sfondo, bordo ed effetti. In ogni categoria vengono fornite informazioni sullo stile. Ad esempio, in Sfondo è possibile specificare Colore sfondo e Immagine e sfumatura.

   * **Avanzate:** Consente di aggiungere CSS personalizzati a un oggetto, che si sovrappone alle proprietà definite dai controlli visivi in caso di sovrapposizione.

   * **Visualizza CSS**: consente di visualizzare il CSS del componente selezionato

  Inoltre, nella barra laterale, in basso è presente una freccia. Facendo clic sulla freccia, si ottengono altre due opzioni: **Simula esito positivo** e **Simula errore.** Queste opzioni, insieme a quelle descritte in precedenza, vengono discusse in dettaglio [sotto](../../forms/using/themes.md#using-rail).

[![Editor temi con barra e quadro evidenziati.](assets/themes.png)](assets/themes-1.png) **R.** Barra laterale **B.** Area di lavoro

### Componenti di stile {#styling-components}

È possibile utilizzare un tema in più moduli adattivi e comunicazioni interattive, per importare la formattazione del componente specificata nel tema. È possibile assegnare stili a vari componenti, ad esempio titoli, descrizioni, pannelli, campi, icone e caselle di testo. I widget consentono di configurare le proprietà dei componenti in un tema. Non è necessario conoscere in precedenza CSS o LESS, ma è preferibile farlo, anche se la sezione CSS Overrides consente di scrivere codice CSS o di fornire selettori personalizzati. La sezione Sostituzioni CSS viene visualizzata quando si seleziona un componente nella barra laterale.

![Componenti eleganti nella barra laterale](assets/stylable-components.png)

Opzioni nella barra laterale che consentono di selezionare e assegnare stili ai diversi componenti.

Facendo clic sul pulsante Modifica in corrispondenza di un componente nella barra laterale, il componente viene selezionato nell’area di lavoro e puoi applicare lo stile al componente utilizzando le opzioni nella barra laterale.

Alcuni componenti come casella di testo, casella numerica, pulsante di scelta e casella di controllo sono classificati in componenti generici come Campo. Ad esempio, si desidera personalizzare lo stile dei pulsanti di scelta. Per selezionare i pulsanti di scelta per lo stile, selezionare **Campo > Widget > Pulsante di opzione**.

Clic **ESPANDI TUTTO** nella barra laterale per visualizzare, seleziona e assegna uno stile ai componenti classificati che non sono visibili in primo piano.

### Layout dei pannelli di stile {#styling-panel-layouts-br}

I temi in AEM Forms supportano lo stile degli elementi nel layout dei pannelli nei moduli e nelle comunicazioni interattive. È supportato lo stile degli elementi nei layout predefiniti e nei layout personalizzati.

I pannelli predefiniti includono:

* Schede a sinistra
* Schede superiori
* Pannello a soffietto
* Responsivo
* Procedura guidata
* Layout mobile

   * Titoli dei pannelli nell’intestazione
   * Senza titoli dei pannelli nell’intestazione

I selettori variano per ciascun layout.
La creazione di stili di layout personalizzati dall’Editor tema prevede:

* Definizione dei componenti di un layout a cui è possibile applicare uno stile e dei selettori CSS per identificare in modo univoco questi componenti
* Definizione delle proprietà CSS che possono essere applicate a questi componenti
* Definire lo stile di questi componenti in modo interattivo dall’interfaccia utente

### Stili diversi per schermi di dimensioni diverse {#different-styles-for-different-screen-sizes-br}

I layout per desktop e dispositivi mobili possono avere stili leggermente o completamente diversi. Per i dispositivi mobili, tablet e telefono condividono layout simili tranne che per le dimensioni dei componenti.

Utilizza i punti di interruzione dell’Editor tema per definire uno stile alternativo per schermi di dimensioni diverse. Potete selezionare un dispositivo di base o una risoluzione sulla quale iniziate a creare il tema e le varianti di stile per altre risoluzioni vengono generate automaticamente. Potete modificare esplicitamente lo stile di tutte le risoluzioni.

>[!NOTE]
>
>Il tema viene creato utilizzando un modulo o una comunicazione interattiva e quindi applicato a diversi moduli o comunicazioni interattive. I punti di interruzione utilizzati nella creazione del tema possono essere diversi dalla forma o dalla comunicazione interattiva a cui è applicato il tema. Le query multimediali CSS si basano sul modulo o sulla comunicazione interattiva utilizzati nella creazione dei temi e non sul modulo o sulla comunicazione interattiva a cui viene applicato il tema.

### Modifica del contesto delle proprietà di stile nella barra laterale durante la selezione degli oggetti {#styling-properties-context-changes-in-sidebar-on-selecting-objects}

Quando selezioni un componente nell’area di lavoro, le relative proprietà di stile vengono elencate nella barra laterale. Selezionare il tipo di oggetto e il relativo stato, quindi specificarne lo stile.

### Stili utilizzati di recente nell’Editor tema {#recently-used-styles-in-theme-editor}

L’editor tema memorizza nella cache fino a 10 stili applicati a un componente. È possibile utilizzare gli stili memorizzati in cache con un altro componente di un tema. Gli stili utilizzati di recente sono disponibili sotto il componente selezionato nella barra laterale come casella di riepilogo. Inizialmente, l’elenco degli stili utilizzati di recente è vuoto.

![libreria di risorse](assets/asset-library.png)

Quando si applica uno stile a un componente, gli stili vengono memorizzati nella cache ed elencati nella casella di riepilogo. In questo esempio, l&#39;etichetta della casella di testo viene formattata in modo da modificare la dimensione e il colore del carattere. Puoi seguire passaggi simili per scegliere un’immagine o modificare i colori per assegnare uno stile a un componente. Osserva come lo stile viene memorizzato nella cache ed elencato nella casella di riepilogo quando viene modificato lo stile dell’etichetta del campo.

![Stile font nella cache per un componente disponibile per un altro](assets/font-style-cached.png)

In questo esempio viene modificato lo stile dell’etichetta del campo e, quando per lo stile è selezionata l’opzione Descrizione pannello reattivo, viene aggiunta una voce di elenco nella libreria delle risorse. La voce nella libreria di risorse può essere utilizzata per modificare lo stile di Descrizione pannello reattivo.

Quando uno stile viene aggiunto nella libreria delle risorse, è disponibile per altri temi e nel [modalità stile](../../forms/using/inline-style-adaptive-forms.md) dell’interfaccia utente dell’editor di moduli o dell’editor di comunicazione interattivo. Allo stesso modo, quando utilizzi la modalità di stile dell’editor di moduli o dell’interfaccia utente dell’editor di comunicazione interattiva per assegnare uno stile a un componente, lo stile viene memorizzato nella cache ed è disponibile nei temi.

Il pulsante più (+) posto accanto alla libreria di risorse consente di salvare in modo permanente lo stile con il nome fornito. Il pulsante più salva lo stile anche se non fai clic sul pulsante Salva nella barra laterale per applicarlo a un componente. Il pulsante più per salvare uno stile da utilizzare successivamente non è disponibile in modalità stile.

![Inserimento di un nome di stile personalizzato per la libreria di risorse](assets/custom-style-name.png)

Quando si specifica un nome personalizzato per uno stile, questo viene associato a un tema e non è più disponibile per altri temi. Per eliminare uno stile salvato:

1. Sulla barra degli strumenti AREA DI LAVORO fare clic su **Opzioni tema** ![theme-options](assets/theme-options.png) > **Gestisci stili**.
1. Nella finestra di dialogo Gestisci stili, seleziona uno stile salvato e fai clic su **Elimina**.

   ![Elimina lo stile salvato](assets/manage-styles.png)

### Anteprima live, salvataggio ed eliminazione delle modifiche {#live-preview-save-and-discard-changes}

Le modifiche apportate allo stile si riflettono immediatamente nella forma o nella comunicazione interattiva caricata nell’area di lavoro. L’anteprima live ti consente di definire e visualizzare in modo interattivo l’impatto dello stile. Quando modifichi lo stile di un componente, il **Fine** nella barra laterale. Per mantenere le modifiche, utilizzare **Fine** pulsante.

>[!NOTE]
>
>Quando si immette un carattere non valido in un campo, il colore del bordo del campo diventa rosso e nell&#39;angolo superiore sinistro dello schermo viene visualizzato un messaggio di errore. Se ad esempio si immettono caratteri alfabetici in una casella di testo che accetta caratteri numerici come input, il colore del bordo della casella di input verrà modificato in rosso. Non puoi salvare un tema di questo tipo senza risolvere l’errore visualizzato nella parte superiore.

### Tema con un altro modulo adattivo o comunicazione interattiva {#theme-with-another-adaptive-form-or-interactive-communication}

Quando si crea un tema, questo viene creato con un modulo fornito con l&#39;Editor tema. In questo modulo viene fornito lo stile dei componenti. Invece del modulo fornito con l’Editor tema, puoi selezionare un modulo o una comunicazione interattiva a tua scelta per assegnargli uno stile e visualizzarne in anteprima i risultati.

Per sostituire il modulo corrente o la comunicazione interattiva nell’area di lavoro dell’Editor temi:

1. Nel pannello EDITOR TEMI, fate clic su **Opzioni tema** ![theme-options](assets/theme-options.png) > **Configura**.

1. Nella scheda Generale, sfoglia e seleziona un modulo o una comunicazione interattiva per il **Modulo/documento adattivo** campo.

### Ripeti/Annulla {#redo-undo}

È possibile annullare o ripristinare le modifiche indesiderate che si verificano accidentalmente. Utilizzare i pulsanti Ripristina/Annulla nell&#39;area di lavoro.

![Azioni Ripristina e Annulla](assets/redo_undo_new.png)

Pulsanti Annulla/Ripristina nell’area di lavoro

I pulsanti Ripristina/Annulla vengono visualizzati quando si applica uno stile a un componente nell’Editor tema.

## Utilizzo dell’Editor tema {#using-the-theme-editor}

L’Editor tema consente di modificare un tema creato o caricato. Accedi a **Forms e documenti > Temi** e selezionare un tema e aprirlo. Il tema viene aperto nell’Editor tema.

Come discusso in precedenza, l’Editor tema dispone di due pannelli: Barra laterale e Area di lavoro.
![theme-editor](assets/theme-editor.png)

Personalizzazione dello stile dello stato di successo del componente Widget casella di testo nell’editor di temi. Il componente è selezionato nell’area di lavoro e il suo stato è selezionato nella barra laterale. Le opzioni di stile disponibili nella barra laterale vengono utilizzate per personalizzare l’aspetto di un componente.

### Utilizzo di Canvas {#using-canvas}

Il tema viene creato utilizzando il modulo predefinito oppure un modulo o una comunicazione interattiva a tua scelta. L’area di lavoro mostra l’anteprima del modulo o della comunicazione interattiva utilizzati per creare il tema con le personalizzazioni specificate in theme. Il righello sopra il modulo viene utilizzato per determinare il layout in base alle dimensioni della visualizzazione del dispositivo.

Nella barra degli strumenti Area di lavoro vengono visualizzati i seguenti elementi:

* **Attiva/Disattiva pannello laterale** ![interruttore-pannello laterale](assets/toggle-side-panel.png): consente di mostrare o nascondere la barra laterale.
* **Opzioni tema** ![theme-options](assets/theme-options.png): fornisce tre opzioni

   * Configura: fornisce opzioni per selezionare il modulo di anteprima o la comunicazione interattiva, Base clientlib e la configurazione di Adobe Fonts.
   * Visualizza CSS tema: genera CSS per il tema selezionato.
   * Gestisci stili: fornisce opzioni per gestire gli stili di testo e immagini
   * Aiuto: esegue una presentazione guidata dell’immagine dell’Editor tema.

* **Emulatore** ![righello](assets/ruler.png): emula l’aspetto del tema per diverse dimensioni di visualizzazione. Una dimensione di visualizzazione viene trattata come punto di interruzione nell’emulatore. È possibile selezionare un punto di interruzione e specificarne uno stile. Ad esempio, Desktop e Tablet sono due punti di interruzione. È possibile specificare stili diversi per ogni punto di interruzione.

Quando selezioni un componente nell’area di lavoro, sopra di esso viene visualizzata la barra degli strumenti del componente. La barra degli strumenti del componente consente di selezionare i componenti o passare a componenti generici. Ad esempio, selezionate una casella di testo numerica in un pannello. Nella barra degli strumenti del componente sono visualizzate le seguenti opzioni:

* **Widget casella numerica**: consente di selezionare il componente per personalizzarne l’aspetto nella barra laterale.
* **Widget campo**: consente di selezionare il componente generico per lo stile. In questo esempio, tutti i componenti di input testo (casella di testo/casella numerica/stepper numerico/input data) sono selezionati per lo stile.

* ![a livello di campo](assets/field-level.png): consente di passare al componente generico per lo stile. Se selezioni la casella numerica e fai clic su questa icona, viene selezionato il componente Campo. Se selezioni il componente Campo e fai clic su questa icona, viene selezionato il pannello. Se continuate a toccare questa icona per selezionarla, finirete per selezionare il layout per lo stile.

>[!NOTE]
>
>Le opzioni disponibili nella barra degli strumenti del componente variano in base al componente selezionato.

![Barra degli strumenti del componente](assets/overlay.png)

Barra degli strumenti dei componenti sulla casella numerica nell’area di lavoro

### Utilizzo di Sidebar {#using-rail}

La barra laterale nell’editor temi fornisce opzioni per personalizzare gli stili dei componenti di un tema e utilizzare i selettori. I selettori consentono di selezionare un gruppo di componenti o di singoli componenti e di cercare i selettori nella barra laterale. Puoi scrivere selettori per i componenti personalizzati.

Quando selezioni un componente dall’area di lavoro o dai selettori nella barra laterale, questa mostra tutte le opzioni che consentono di personalizzare gli stili.
Di seguito sono riportate le opzioni visualizzate nella barra laterale quando si seleziona un componente:

* Stato
* Foglio delle proprietà
* Simula errore/esito positivo

#### Stato {#state}

Uno stato è un indicatore dell’interazione dell’utente con un componente. Ad esempio, quando un utente immette dati errati in una casella di testo, lo stato della casella di testo cambia in errore. L’editor tema consente di specificare lo stile per un particolare stato.

Le opzioni per la personalizzazione degli stili di stato variano a seconda dei componenti.

#### Foglio delle proprietà {#property-sheet}

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Utilizzare</strong></td>
  </tr>
  <tr>
   <td><p>Dimensioni e posizione</p> </td>
   <td><p>Consente di applicare stili a allineamento, dimensioni, posizionamento e posizionamento dei componenti nel tema. </p> <p>Le opzioni disponibili sono l'impostazione di visualizzazione, la spaziatura interna, il margine, la larghezza, l'altezza e l'indice Z.</p> <p>È inoltre possibile utilizzare la modalità Layout per definire la larghezza dei componenti mediante una semplice interfaccia con metodo di trascinamento. Per ulteriori informazioni, consulta <a href="../../forms/using/resize-using-layout-mode.md">Utilizzare la modalità Layout per ridimensionare i componenti</a>.</p> </td>
  </tr>
  <tr>
   <td><p>Testo</p> </td>
   <td><p>Consente di personalizzare gli stili di testo nel componente del tema.</p> <p>Si desidera ad esempio modificare l'aspetto del testo immesso nella casella di testo.</p> <p>Le opzioni disponibili sono famiglia di caratteri, peso, colore, dimensione, altezza linea, allineamento testo, spaziatura, rientro testo, sottolineatura, corsivo, trasformazione testo, allineamento verticale, linea di base e direzione. </p> </td>
  </tr>
  <tr>
   <td><p>Informazioni di base </p> </td>
   <td><p>Consente di riempire lo sfondo del componente con un’immagine o un colore. </p> </td>
  </tr>
  <tr>
   <td><p>Bordo</p> </td>
   <td><p>Consente di scegliere il bordo del componente. Ad esempio, si desidera che la casella di testo abbia un bordo rosso intenso con una linea tratteggiata. </p> <p>Le opzioni disponibili sono larghezza, stile, raggio e colore del bordo.</p> </td>
  </tr>
  <tr>
   <td><p>Effetti</p> </td>
   <td><p>Consente di aggiungere effetti speciali ai componenti quali opacità, modalità di fusione e ombre. </p> </td>
  </tr>
  <tr>
   <td><p>Avanzate </p> </td>
   <td><p>Consente di aggiungere:</p>
    <ul>
     <li>Proprietà per <code>::before</code> e <code>::after</code> pseudo elementi per aggiungere contenuto dopo o prima del contenuto predefinito nel selettore e assegnarvi uno stile.<br /> Consulta <a href="https://www.w3schools.com/css/css_pseudo_elements.asp" target="_blank">Pseudo-elementi CSS</a>.</li>
     <li>Codice CSS personalizzato in linea con un componente e scrivi selettori personalizzati. </li>
    </ul> <p>Quando aggiungi un codice CSS personalizzato, questo sovrascrive la personalizzazione aggiunta utilizzando le opzioni nella barra laterale. </p> </td>
  </tr>
 </tbody>
</table>

#### Simula errore/esito positivo {#simulate-error-success}

Le opzioni Simula errore e Riuscito sono disponibili nella parte inferiore della barra laterale. Puoi visualizzarli utilizzando una freccia mostra/nascondi visibile nella parte inferiore della barra laterale. L’Editor tema consente di applicare stili a vari stati di un componente.

Ad esempio, è possibile aggiungere un campo numerico nel modulo e specificarne lo stile nell&#39;editor temi. Quando un utente digita un valore alfanumerico nel campo, si desidera modificare il colore di sfondo della casella di testo. Seleziona il campo numerico nel tema e utilizza l’opzione stato nella barra laterale. Selezionare lo stato Errore nella barra laterale e cambiare il colore di sfondo in rosso. Per visualizzare in anteprima il comportamento, puoi utilizzare l’opzione Simula errore disponibile nella barra laterale. Le opzioni Simula errore e Successo sono descritte in dettaglio di seguito:

* **Simula esito positivo**: consente di visualizzare l’aspetto di un componente se ne specifichi lo stile per lo stato di successo. Ad esempio, in un modulo, i clienti impostano la password. Gli utenti possono impostare la password in base alle linee guida fornite. Quando un utente digita una password seguendo tutte le linee guida fornite, la casella di testo diventa verde. Quando la casella di testo diventa verde, lo stato è Completato. Potete specificare lo stile di un componente in stato di successo e simularne l&#39;aspetto utilizzando l&#39;opzione Simula successo (Simulate Success).

* **Simula errore**: consente di visualizzare l’aspetto di un componente se ne specifichi lo stile per lo stato di errore. Ad esempio, in un modulo, i clienti impostano la password. Gli utenti possono impostare la password in base alle linee guida fornite. Quando un utente digita una password che non segue tutte le linee guida fornite, la casella di testo diventa rossa. Quando la casella di testo diventa rossa, si trova nello stato di errore. Potete specificare lo stile di un componente in stato di errore e simularne l&#39;aspetto utilizzando l&#39;opzione Simula errore (Simulate Error).

### Applicazione di uno stile a un componente {#styling-a-component}

Ad esempio, nel modulo sono disponibili due tipi di caselle di testo: una che accetta solo valori numerici e l&#39;altra che accetta valori alfanumerici. È possibile personalizzare lo stile della casella di testo che accetta solo valori numerici, ovvero una casella numerica.

Per personalizzare lo stile di un particolare componente (in questo esempio, una casella numerica), effettua le seguenti operazioni:

1. Nell’Editor temi, seleziona la casella numerica nell’area di lavoro.
1. Quando selezioni la casella numerica, puoi visualizzare la barra degli strumenti del componente con tre opzioni:

   * **Widget casella numerica**
   * **Widget campo** ![a livello di campo](assets/field-level.png)

1. Seleziona **Widget casella numerica**.
1. Il titolo della barra laterale diventa Widget casella numerica e mostra le opzioni per personalizzarne l’aspetto.
Utilizzare **Dimension e posizione** nella barra laterale per personalizzare le dimensioni del componente. Assicurati che lo stato sia **Predefinito**.

Invece di selezionare **Widget casella numerica**, seleziona **Widget campo** nella barra degli strumenti del componente ed esegui i passaggi indicati sopra. Quando selezionate le quote per **Widget campo** , tutte le caselle di testo tranne la casella numerica hanno le stesse dimensioni.

### Campi di stile per un determinato stato {#styling-fields-given-state}

La barra degli strumenti del componente consente inoltre di specificare lo stile dei componenti in base ai diversi stati. Ad esempio, se un componente è disabilitato, si trova nello stato disabilitato. Gli stati comunemente utilizzati di un componente a cui è possibile applicare uno stile nell’editor di temi sono: Predefinito, Attiva, Disattivato, Errore, Operazione riuscita e Passaggio del mouse. Puoi selezionare un componente nell’area di lavoro e utilizzare l’opzione Stato nella barra laterale per personalizzarne l’aspetto.

Per personalizzare lo stile di un componente in uno stato specifico, effettua le seguenti operazioni:

1. Seleziona un componente nell’area di lavoro, quindi seleziona l’opzione appropriata dalla barra degli strumenti del componente.
La barra laterale mostra le opzioni per personalizzare lo stile del componente.
1. Seleziona uno stato nella barra laterale. Ad esempio, Stato di errore.
1. Utilizzare opzioni quali **Bordo, sfondo** nella barra laterale per personalizzare l’aspetto del componente.
1. Utilizza il **Simula errore** nella parte inferiore della barra laterale per visualizzare l’aspetto dello stile durante la modifica.

Quando personalizzi lo stile di un componente dopo averne specificato lo stato, la personalizzazione viene visualizzata solo per il componente per lo stato specificato. Ad esempio, se personalizzi lo stile del componente quando si seleziona lo stato del passaggio del mouse. La personalizzazione viene visualizzata per il componente quando si sposta il puntatore sul componente nel modulo renderizzato o nella comunicazione interattiva a cui si applica il tema.

Per simulare il comportamento di stati diversi da errore e successo, utilizzate la modalità Anteprima. Per utilizzare la modalità Anteprima, fare clic su **Anteprima** nella barra degli strumenti della pagina.

### Layout degli stili per schermi più piccoli {#styling-layouts-for-smaller-displays}

Utilizza righello nell’area di lavoro per selezionare i punti di interruzione per i dispositivi con schermi più piccoli. Fai clic sull’emulatore ![righello](assets/ruler.png) nell&#39;area di lavoro per visualizzare il righello e i punti di interruzione. I punti di interruzione consentono di visualizzare in anteprima un modulo o una comunicazione interattiva per dimensioni di visualizzazione relative a dispositivi diversi, ad esempio telefoni e tablet. Nell’Editor tema sono supportate più dimensioni di visualizzazione.

Per assegnare uno stile ai componenti per punti di interruzione diversi:

1. Nell&#39;area di lavoro selezionare un punto di interruzione sopra il righello.
Un punto di interruzione rappresenta un dispositivo mobile e le relative dimensioni di visualizzazione.
1. Utilizza la barra laterale per personalizzare lo stile dei componenti del modulo o della comunicazione interattiva nel tema in base alle dimensioni di visualizzazione selezionate.
1. Assicurati che la personalizzazione sia salvata.

Puoi assegnare uno stile ai componenti di comunicazione interattiva o di modulo per più dispositivi. I componenti per moduli e comunicazioni interattive per desktop e dispositivi mobili possono avere stili completamente diversi.

### Utilizzo di font per web in un tema {#using-web-fonts-in-a-theme}

È ora possibile utilizzare i font disponibili in un servizio web in un modulo adattivo o in una comunicazione interattiva. Pronti all’uso, [Adobe Fonts](https://fonts.adobe.com/), servizio font per web di Adobe, è disponibile come configurazione. Per utilizzare Adobe Fonts, crea un kit, aggiungi font al suo interno e ottieni l’ID kit da [Adobe Fonts](https://fonts.adobe.com/).

Per configurare Adobe Fonts nell’AEM, effettua le seguenti operazioni:

1. Nell’istanza di authoring, fai clic su ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Strumenti ![martello](assets/hammer.png) > Implementazione > Cloud Service.
1. Il giorno **Cloud Service** , passa alla pagina e apri la **Adobe Fonts** opzione. Apri la cartella di configurazione e fai clic su **Crea**.
1. Il giorno **Crea configurazione** , specifica un titolo per la configurazione e fai clic su **Crea**.

   Ti reindirizzano alla pagina di configurazione.

1. Nella finestra di dialogo Modifica componente visualizzata, specifica l’ID del kit e fai clic su **OK**.

Per configurare un tema per l’utilizzo della configurazione di Adobe Fonts, effettua le seguenti operazioni:

1. Nell’istanza dell’autore, apri un tema nell’editor di temi.
1. Nell’editor temi, passa a **Opzioni tema** ![theme-options](assets/theme-options.png) > **Configura**.
1. In entrata **Configurazione Adobe Fonts** , selezionare un kit e fare clic su **Salva**.

   Ora è possibile vedere che i font vengono aggiunti nella proprietà font-family del tema.

### Visualizzazione e selezione di tipi di carattere nell&#39;editor temi {#listing-and-selecting-fonts-in-theme-editor}

Puoi utilizzare il servizio di configurazione del tema per aggiungere più font all’editor del tema. Per aggiungere font, effettuate le seguenti operazioni:

1. Accedi alla console web AEM con privilegi di amministratore. L’URL per la console web AEM è `https://'[server]:[port]'/system/console/configMgr`.
1. Apri **Servizio di configurazione tema modulo adattivo**.

   ![theme-config](assets/theme-config.png)

1. Fate clic su +, specificate il nome del font e fate clic su **Salva**. Il font viene aggiunto e disponibile nell’editor temi.

#### Selezione di tipi di carattere nell&#39;editor temi {#selecting-fonts-in-theme-editor}

È possibile utilizzare il pulsante + per aggiungere un carattere. Quando si aggiunge un carattere, questo viene elencato nella barra laterale.

![Nuovo font elencato nell’editor temi](assets/theme-font.png)

Oltre all’opzione di configurazione del tema, puoi anche aggiungere il font dall’editor stesso. Digitate il font da usare nel campo famiglia font sotto la barra laterale e premete il tasto Invio sulla tastiera.

![Digitazione e selezione del font nell’editor temi](assets/font-selection.png)

Quando selezionate un carattere, questo viene aggiunto all&#39;elenco della famiglia di caratteri. Potete utilizzare l&#39;opzione Maschera (Mask) nell&#39;editor temi per disattivare o attivare i font elencati.

![caratteri multipli](assets/multi-fonts.jpg)

È possibile visualizzare il cambiamento del carattere del componente.

Il campo Famiglia di caratteri supporta più tipi di carattere. Quando digitate un font, il browser lo cerca e lo applica al componente selezionato. Se il browser non è in grado di trovare un carattere, cerca un carattere accanto ad esso nella famiglia. È possibile iniziare digitando il tipo di carattere specifico desiderato. Se non si trova il carattere da utilizzare, è possibile digitare un carattere generico nella famiglia e utilizzarlo.

#### Stili di maschera applicati nell’editor temi {#mask-styles-applied-in-theme-editor}

È possibile mascherare gli stili applicati a un tema. Nella barra laterale dell’editor del tema, puoi utilizzare ![toggle_eye](assets/toggle_eye.png)per disattivare uno stile applicato. Ad esempio, se modifichi le dimensioni di un componente in una maschera o in una comunicazione interattiva, puoi utilizzare il pulsante Maschera a sinistra di una proprietà per disabilitarlo. Quando salvate un tema, le opzioni di mascheramento selezionate vengono mantenute.

![Opzione Maschera disponibile nella barra laterale dell’editor temi](assets/mask-styles.png)

L’esempio seguente mostra gli stili mascherati e non mascherati in un tema.

![Stili mascherati e non mascherati](assets/mask2.png)

## Applicazione di un tema a un modulo o a una comunicazione interattiva {#applying-a-theme-to-a-form-or-interactive-communication-br}

Per applicare un tema a un modulo adattivo:

1. Apri il modulo in modalità di modifica. Per aprire un modulo in modalità di modifica, selezionarlo e fare clic su **Apri**.
1. In modalità di modifica, seleziona un componente, quindi fai clic su ![a livello di campo](assets/field-level.png) > **Contenitore modulo adattivo** e quindi fare clic su ![cmppr](assets/cmppr.png).

   È possibile modificare le proprietà del modulo nella barra laterale.

1. Nella barra laterale, fai clic su **Stile**.
1. Seleziona il tema da **Tema modulo adattivo** e fai clic su **Fine** ![pulsante di controllo](assets/check-button.png).

Per applicare un tema a una comunicazione interattiva:

1. Apri la comunicazione interattiva in modalità di modifica. Per aprire una comunicazione interattiva in modalità di modifica, seleziona un modulo e fai clic su **Apri**.
1. In modalità di modifica, seleziona un componente, quindi fai clic su ![a livello di campo](assets/field-level.png) >**Contenitore documento** e quindi fare clic su ![cmppr](assets/cmppr.png).

   È possibile modificare le proprietà del modulo nella barra laterale.

1. Nella barra laterale, sotto **Base**, seleziona il tema dall&#39;elenco **Tema** e fai clic su **Fine** ![pulsante di controllo](assets/check-button.png)

### Modificare il tema di un modulo in fase di esecuzione {#change-theme-of-a-form-at-runtime}

Un tema consente di applicare uno stile ai diversi componenti di un modulo. È possibile utilizzare `themeOverride` per modificare dinamicamente il tema di una maschera. Un URL tipico di un modulo è:

`https://<server>:<port>/content/forms/af/test.html`

È possibile utilizzare il parametro themeOverride per applicare un tema in fase di esecuzione.

`https://<server>:<port>/content/forms/af/test.html?themeOverride=/content/dam/formsanddocuments-themes/simpleEnrollmentTheme`

Il `themeOverride` consente di fornire un percorso a un tema. Cambia il tema del modulo e lo aggiorna con stili aggiornati.

## Ottenere un aspetto specifico utilizzando i temi {#specific-af-appearance}

Con AEM Forms, oltre al tema predefinito dell’area di lavoro, esistono molti altri temi. Se si desidera progettare il modulo o la comunicazione interattiva utilizzando altri temi, oltre a ulteriori modifiche, copiare il tema dalla cartella Libreria temi. Incollare i temi copiati all&#39;esterno della cartella Libreria temi e modificare il tema copiato in base alle modifiche desiderate.

Per copiare un tema, effettuare le seguenti operazioni:

1. Nell’istanza di authoring, passa a **Adobe Experience Manager > Forms > Temi**.
1. Aprire la cartella Libreria temi.
1. Nella cartella Libreria temi, passa il puntatore sul tema predefinito corrispondente e seleziona **Copia**.
1. Incollare il tema copiato all&#39;esterno della cartella Libreria temi.
1. Personalizza il tema copiato.

Dopo aver personalizzato il tema, applicalo al modulo o alla comunicazione interattiva.

>[!NOTE]
>
>Non modificare i temi disponibili nella cartella Libreria temi. Questa cartella contiene i temi di sistema. Qualsiasi modifica apportata a questi temi viene sovrascritta durante l’installazione di una versione più recente o di una correzione rapida di AEM Forms.

## Impatto su altri casi di utilizzo di moduli adattivi {#impact-on-other-adaptive-form-use-cases}

* **Pubblicare/annullare la pubblicazione di un modulo:** Quando si pubblica un modulo, viene pubblicato anche il tema applicato a (se non è già pubblicato)
* **Importare/esportare un modulo:** Quando si importa o si esporta un modulo, viene automaticamente importato o esportato anche il tema associato.
* **Riferimenti di un modulo:** La sezione Riferimenti nei riferimenti del modulo contiene una voce aggiuntiva per il tema.
* **Ora ultima modifica di un modulo:** Aggiornato quando il tema associato viene modificato.
* **Test A/B:** È possibile applicare un tema diverso a due versioni del modulo in un test A/B. Le informazioni dei due temi vengono memorizzate singolarmente nei due contenitori guida.

## Sequenza di generazione CSS {#css-generation-sequence}

Quando selezioni Visualizza CSS, l’Editor tema raccoglie tutte le informazioni sullo stile e crea un CSS. Raccoglie le informazioni nel seguente ordine:

1. Stile definito nella libreria client di base del tema.
1. Stile definito dall’utente, specificato utilizzando le proprietà nella barra laterale.
1. Stile CSS fornito utilizzando l’opzione CSS Override.

Ad esempio, il colore di sfondo di una casella di testo è blu nella libreria client di base. La modifica in rosa utilizzando le proprietà nella barra laterale. Quando si genera CSS, il colore di sfondo della casella di testo viene visualizzato come rosa. Dopo aver modificato il colore di sfondo utilizzando le proprietà, un altro autore utilizza l’opzione CSS override per modificare la casella di testo del colore di sfondo come bianco. Quando generi CSS, il colore di sfondo viene visualizzato come bianco nel CSS generato.

## Debug degli stili {#debugging-styles}

Quando si specificano gli stili per i componenti nell’Editor tema, viene generato un CSS. Quando si applica uno stile a un componente generico, viene applicato lo stile anche a più componenti inclusi in esso. Ad esempio, quando si applica uno stile a un campo, viene applicato anche lo stile alla casella di testo e all&#39;etichetta in esso contenuta. Quando si applica uno stile alla casella di testo all’interno del campo, viene applicato un proprio CSS. Se desideri eseguire il debug del CSS generato per il campo e il componente, l’Editor tema fornisce opzioni che ti consentono di visualizzare il CSS.

Puoi visualizzare il CSS generato utilizzando le seguenti opzioni:

* **Visualizza CSS** opzione nella barra laterale: quando selezioni un componente nel tema, puoi visualizzare l’opzione VISUALIZZA CSS nella barra laterale. Mostra il CSS generato, incluso il CSS per `::before` e `::after` pseudo elementi.
* **Visualizza CSS tema** nella barra degli strumenti dell’area di lavoro: nella barra degli strumenti dell’area di lavoro, fai clic su ![theme-options](assets/theme-options.png) > **Visualizza CSS tema**. Puoi visualizzare l’intero CSS del tema generato dalle proprietà definite nell’Editor tema.

## Risoluzione dei problemi, raccomandazioni e best practice {#troubleshooting-recommendations-and-best-practices}

* **Evitare risorse da un altro tema**

  Quando modifichi un tema, puoi sfogliare e aggiungere risorse (come immagini) da altri temi. Ad esempio, stai modificando lo sfondo di una pagina. Ad esempio, quando selezioni **Pagina** ![edit-button](assets/edit-button.png)> **Sfondo** > **Aggiungi** > **Immagine**, viene visualizzata una finestra di dialogo che consente di sfogliare e aggiungere immagini in un altro tema.

* Se una risorsa viene aggiunta da un altro tema e l’altro tema viene spostato o eliminato, puoi riscontrare dei problemi con il tema corrente. Si consiglia di evitare di sfogliare e aggiungere risorse da altri temi.
* **Utilizzo di base clientlib, editor temi e stile in linea**

   * **Base clientlib**:

     La libreria client di base contiene informazioni sullo stile. Per utilizzare le informazioni sullo stile nelle librerie lato client nei temi.

      1. Accedi a **Experience Manager > Forms > Temi**.
      1. Nella pagina Temi selezionare un tema e fare clic su **Visualizza proprietà**.
      1. Nella pagina Proprietà visualizzata, fai clic su **Avanzate**.
      1. Nella scheda Avanzate, individua e seleziona la libreria client da utilizzare nel campo Posizione libreria client.
      1. Fai clic su **Salva**.

     Lo stile specificato nella libreria client viene importato nel tema che lo utilizza. Ad esempio, è possibile specificare lo stile per la casella di testo, la casella numerica e il cambio nella libreria client. Quando si importa la libreria client nel tema, viene importato lo stile della casella di testo, della casella numerica e del commutatore. Puoi quindi assegnare uno stile ad altri componenti utilizzando l’editor di temi.
Puoi anche creare un tema, crearne copie e quindi modificare lo stile fornito nei temi copiati per casi d’uso simili.
Consulta [Ottenere un aspetto specifico utilizzando i temi](#specific-af-appearance)

   * **Editor temi:**

     L’Editor tema consente di creare temi per formattare il modulo o la comunicazione interattiva. È possibile specificare lo stile dei componenti di un tema, che consente di conferire un aspetto uniforme a più moduli o comunicazioni interattive sviluppate dall&#39;utente. Si consiglia di specificare le informazioni sullo stile in un tema e quindi di applicare il tema a un modulo.

   * **Stile in linea:**

     È possibile assegnare uno stile ai componenti utilizzando la modalità Stile nell&#39;editor multicanale di moduli o comunicazioni interattive quando si utilizza un modulo. L’utilizzo della modalità stile per modificare lo stile dei componenti del modulo sovrascrive lo stile specificato nel tema. Per modificare lo stile di alcuni componenti di un modulo specifico, vedere [Stile in linea dei componenti](../../forms/using/inline-style-adaptive-forms.md).

* **Utilizzo delle librerie lato client**

  Se desideri creare librerie client per importare informazioni sullo stile, consulta [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md). Dopo aver creato una libreria client, puoi importarla nel tema seguendo i passaggi indicati sopra.

* **Modifica della larghezza del layout del pannello contenitore**

  La modifica della larghezza del layout del pannello contenitore non è consigliata. Quando si specifica la larghezza di un pannello contenitore, questo diventa statico e non si adatta a visualizzazioni diverse.

* **Quando utilizzare l’editor moduli o l’editor temi per lavorare con intestazione e piè di pagina**

  Utilizzare l&#39;editor tema se si desidera applicare uno stile a intestazione e piè di pagina utilizzando opzioni di stile quali stile, sfondo e trasparenza del carattere.
Se si desidera fornire informazioni quali un&#39;immagine del logo, il nome della società nell&#39;intestazione e le informazioni sul copyright nel piè di pagina, utilizzare le opzioni dell&#39;editor di moduli.
