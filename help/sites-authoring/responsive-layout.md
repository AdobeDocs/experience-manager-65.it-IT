---
title: Layout reattivo
seo-title: Responsive Layout
description: AEM consente di realizzare un layout reattivo per le pagine
seo-description: AEM allows you to realize a responsive layout for your pages
uuid: 4db45d78-9fca-4251-b504-ae3481fd9a8b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 668d1a8a-c757-4c9f-833f-e5dada4d0384
exl-id: 760b8419-5cf8-49c5-8d4f-6691f5256c53
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1782'
ht-degree: 93%

---

# Layout reattivo  {#responsive-layout}

AEM consente di creare un layout reattivo per le pagine mediante il componente **Contenitore di layout**.

Questo fornisce un sistema paragrafo che consente di posizionare i componenti all’interno di una griglia reattiva. Con questa griglia è possibile riorganizzare il layout in base alla dimensione e al formato del dispositivo o della finestra. Il componente viene utilizzato [**insieme alla modalità** Layout](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode), che consente di creare e modificare il layout reattivo (o dinamico) in base al dispositivo.

Il Contenitore di layout:

* Fornisce ancoraggio orizzontale sulla griglia, unitamente alla possibilità di posizionare componenti affiancati sulla griglia e definire quando dovrebbero venire compressi/ridisposti.
* Utilizza punti di interruzione predefiniti (ad es. per smartphone, tablet ecc.) per definire il comportamento del contenuto per i relativi dispositivi e orientamenti.

   * Ad esempio, puoi personalizzare le dimensioni del componente o specificare se il componente può essere visualizzato su dispositivi specifici.

* Può essere nidificato per abilitare il controllo delle colonne.

L’utente può quindi visualizzare quale sarà l’aspetto dei contenuti per dispositivi specifici utilizzando l’emulatore.

>[!CAUTION]
>
>Il componente Contenitore di layout è disponibile anche nell’interfaccia classica, ma le sue funzionalità complete sono supportate e disponibili solo nell’interfaccia touch.

AEM consente di realizzare il layout dinamico per le pagine utilizzando una combinazione di meccanismi:

* Componente [**Contenitore di layout**](#adding-a-layout-container-and-its-content-edit-mode)

   Questo componente è disponibile nel [browser dei componenti](/help/sites-authoring/author-environment-tools.md#components-browser) e fornisce un sistema paragrafo a griglia che consente di aggiungere e posizionare i componenti all’interno di una griglia dinamica. Può essere impostato anche come sistema paragrafo predefinito sulla tua pagina.

* [**Modalità Layout**](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)

   Una volta che il Contenitore di layout è collocato nella pagina, è possibile utilizzare la modalità di **Layout** per posizionare i contenuti all’interno della griglia dinamica.

* [**Emulatore**](#selecting-a-device-to-emulate)
Consente di creare e modificare siti web dinamici il cui layout si riorganizza in base alle dimensioni del dispositivo o della finestra, ridimensionando i componenti in modo interattivo. L’utente può quindi visualizzare quale sarà l’aspetto dei contenuti utilizzando l’emulatore.

Con questi meccanismi basati su una griglia reattiva è possibile:

* Utilizzare i punti di interruzione per definire il layout di contenuti diversi in base alla larghezza del dispositivo (in relazione al tipo di dispositivo e all’orientamento).
* Utilizzare questi stessi punti di interruzione e layout di contenuti per assicurare che il contenuto sia dinamico rispetto alle dimensioni della finestra del browser sul desktop.
* Utilizzare l’ancoraggio orizzontale sulla griglia per posizionarvi i componenti, ridimensionarli, definire quando dovrebbero venire compressi o ridisposti in modo da risultare affiancati o sovrapposti.
* Nascondere componenti per layout di dispositivo specifici.
* Gestire il controllo delle colonne.

A seconda del progetto, il Contenitore di layout può essere usato come il sistema paragrafo predefinito per le pagine o come componente disponibile per essere aggiunto alla pagina tramite il browser Componenti (o entrambi).

>[!NOTE]
>
>Adobe fornisce la [documentazione GitHub](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) relativa al layout dinamico come riferimento per gli sviluppatori front-end, consentendo loro di utilizzare la griglia di AEM fuori da AEM, ad esempio quando si crea uno schema HTML statico per un futuro sito AEM.

>[!NOTE]
>
>L’uso dei meccanismi di cui sopra è abilitato mediante la configurazione del modello. Vedi [Configurazione del layout reattivo](/help/sites-administering/configuring-responsive-layout.md) per ulteriori informazioni.

## Definizioni di layout, emulazione del dispositivo e punti di interruzione {#layout-definitions-device-emulation-and-breakpoints}

Quando si crea il contenuto del sito web è importante assicurarsi che venga visualizzato in modo adatto al dispositivo utilizzato.

AEM consente di definire layout dipendenti dalla larghezza del dispositivo:

* L’emulatore consente di emulare i layout su una gamma di dispositivi. Oltre al tipo di dispositivo, anche l’orientamento impostato dall’opzione **Ruota dispositivo** può influenzare il punto di interruzione che viene selezionato quando cambia la larghezza.
* I punti di interruzione sono i punti che separano le definizioni di layout.

   * Essi definiscono a tutti gli effetti la larghezza massima (in pixel) di qualsiasi dispositivo che utilizza un layout specifico.
   * I punti di interruzione sono normalmente applicabili a una gamma di dispositivi, in base alla larghezza del relativo schermo.
   * La portata di un punto di interruzione si estende a sinistra fino al punto di interruzione successivo.
   * Non è possibile selezionare specificatamente un punto di interruzione: la selezione di un dispositivo e di un orientamento comporterà la selezione automatica del punto di interruzione adeguato.

Il dispositivo **Desktop** è privo di una larghezza specifica e fa riferimento al punto di interruzione predefinito (ovvero tutto quanto si trova oltre l’ultimo punto di interruzione configurato).

>[!NOTE]
>
>È teoricamente possibile definire punti di interruzione per ogni singolo dispositivo, ma questo rende decisamente più macchinose la definizione e la manutenzione dei layout.

Quando utilizzi l’emulatore e selezioni un dispositivo specifico per l’emulazione, la definizione del layout e il relativo punto di interruzione vengono evidenziati. Eventuali modifiche apportate al layout verranno riconosciute per altri dispositivi su cui si applica il punto di interruzione, ovvero qualsiasi dispositivo disponibile a sinistra del marcatore del punto di interruzione attivo, ma prima del marcatore del punto di interruzione successivo.

Ad esempio, se selezioni il dispositivo **iPhone 6 Plus** (con una larghezza di 540 pixel) per l’emulazione e il layout, verrà attivato anche il punto di interruzione **Telefono** (definito con 768 pixel). Tutte le modifiche di layout apportate per **iPhone 6** diverranno applicabili per altri dispositivi nel punto di interruzione **Telefoni**, come **iPhone 5** (definito con 320 pixel).

![screen_shot_2018-03-23at084058](assets/screen_shot_2018-03-23at084058.png)

## Selezione di un dispositivo da emulare {#selecting-a-device-to-emulate}

1. Apri la pagina desiderata per la modifica. Ad esempio:

   `http://localhost:4502/editor.html/content/we-retail/us/en/experience.html`

1. Seleziona l’icona **Emulatore** sulla barra degli strumenti in alto:

   ![](do-not-localize/screen_shot_2018-03-23at084256.png)

1. Viene aperta la barra degli strumenti dell’emulatore.

   ![screen_shot_2018-03-23at084551](assets/screen_shot_2018-03-23at084551.png)

   La barra degli strumenti dell’emulatore mostra le seguenti opzioni di layout aggiuntive:

   * **Ruota dispositivo**: consente di ruotare l’orientamento di un dispositivo da verticale a orizzontale e viceversa.

   ![](do-not-localize/screen_shot_2018-03-23at084612.png) ![](do-not-localize/screen_shot_2018-03-23at084637.png)

   * **Seleziona il dispositivo**: consente di definire un dispositivo specifico da emulare da un elenco (ved. il passaggio successivo).

   ![](do-not-localize/screen_shot_2018-03-23at084743.png)

1. Per selezionare un dispositivo specifico da emulare è possibile:

   * Utilizzare l’icona Seleziona il dispositivo e scegliere il dispositivo dal selettore a discesa.
   * Toccare o fare clic sull’indicatore del dispositivo nella barra degli strumenti dell’emulatore.

   ![screen_shot_2018-03-23at084818](assets/screen_shot_2018-03-23at084818.png)

1. Una volta che un dispositivo specifico è stato selezionato è possibile:

   * Visualizzare il marcatore attivo per il dispositivo selezionato, ad esempio **iPad.**
   * Visualizzare il marcatore attivo per il [punto di interruzione](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) adeguato, ad esempio **Tablet**.

   ![screen_shot_2018-03-23at084932](assets/screen_shot_2018-03-23at084932.png)

   * La linea punteggiata blu rappresenta la *piega* per il dispositivo selezionato (qui un **iPhone 6)**.

   ![screen_shot_2018-03-23at084947](assets/screen_shot_2018-03-23at084947.png)

   * La piega può essere anche considerata l’interruzione di riga della pagina (da non confondere con i [punti di interruzione](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)) per il contenuto. Questa è visualizzata per comodità, per mostrare quale parte del contenuto è visibile all’utente sul dispositivo prima di scorrere in basso.
   * La riga della piega non viene visualizzata se l’altezza del dispositivo emulato è superiore alle dimensioni dello schermo.
   * La piega è indicata per comodità dell’autore e non viene visualizzata nella pagina pubblicata.



## Aggiunta di un contenitore di layout e del relativo contenuto (modalità di modifica) {#adding-a-layout-container-and-its-content-edit-mode}

Un **Contenitore di layout** è un sistema paragrafo che:

* Include altri componenti.
* Definisce il layout.
* Risponde alle modifiche.

>[!NOTE]
>
>Se non è già disponibile, il **Contenitore di layout** deve essere [attivato esplicitamente per un sistema paragrafo/pagina](/help/sites-administering/configuring-responsive-layout.md) (ad esempio, utilizzando la modalità [**Progettazione**).](/help/sites-authoring/default-components-designmode.md)

1. Il **Contenitore di layout** è disponibile come componente standard nel [browser componenti](/help/sites-authoring/author-environment-tools.md#components-browser). Da qui è possibile trascinarlo nella posizione desiderata sulla pagina, dopodiché verrà visualizzato il segnaposto **Trascina qui i componenti**.
1. È quindi possibile aggiungere componenti al Contenitore di layout. Questi componenti includeranno il contenuto vero e proprio:

   ![screen_shot_2018-03-23at085500](assets/screen_shot_2018-03-23at085500.png)

## Selezione e intervento su un Contenitore di layout (modalità di modifica) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Come con altri componenti, puoi selezionare e quindi intervenire (opzioni Copia, Taglia, Elimina) su un Contenitore di layout (in modalità di **modifica**):

>[!CAUTION]
>
>Dato che un Contenitore di layout è un sistema paragrafo, la sua eliminazione comporta l’eliminazione della griglia di layout e di tutti i componenti (e relativo contenuto) inclusi all’interno del contenitore.

1. Se passi il cursore del mouse o tocchi il segnaposto di una griglia, viene visualizzato il menu delle azioni.

   ![screen_shot_2018-03-23at085357](assets/screen_shot_2018-03-23at085357.png)

   È necessario selezionare l’opzione **Elemento padre**.

   ![](do-not-localize/screen_shot_2018-03-23at085417.png)

1. Se il componente del layout è nidificato, seleziona l’opzione **Elemento padre** per avere una selezione a discesa, che consente di selezionare il contenitore nidificato del layout o il relativo elemento padre.

   Quando passi il cursore del mouse sui nomi dei contenitori nel menu a discesa, sulla pagina vengono visualizzati i relativi contorni.

   * Il contenitore di layout nidificato inferiore presenta un contorno nero.
   * Il contenitore di layout nidificato inferiore successivo è contornato in grigio scuro.
   * Ogni contenitore successivo viene visualizzato in una tonalità di grigio più chiara.

   ![screen_shot_2018-03-23at085636](assets/screen_shot_2018-03-23at085636.png)

1. In questo modo viene messa evidenziata l’intera griglia con il relativo contenuto. Viene visualizzata la barra degli strumenti delle azioni, da cui è possibile selezionare un’azione, ad esempio **Elimina**.

   ![screen_shot_2018-03-23at085724](assets/screen_shot_2018-03-23at085724.png)

## Definire un layout (modalità Layout) {#defining-layouts-layout-mode}

>[!NOTE]
>
>È possibile definire un layout distinto per ogni [punto di interruzione](#layout-definitions-device-emulation-and-breakpoints) (come determinato dal tipo di dispositivo e dall’orientamento emulati).

Per configurare il layout di una griglia dinamica implementato con il contenitore di layout è necessario utilizzare la modalità **Layout**.

La modalità **Layout** può essere avviata in due modi.

* Utilizzando il menu [modalità nella barra degli strumenti](/help/sites-authoring/author-environment-tools.md#page-modes) e selezionando la modalità **Layout**

   * Seleziona la modalità **Layout** esattamente come si fa per passare alla modalità **Modifica** o **Impostazione destinazione**.
   * La modalità **Layout** rimane persistente; si esce dalla modalità **Layout** solo quando si seleziona un’altra modalità mediante il selettore di modalità.

* Quando [si modifica un singolo componente.](/help/sites-authoring/editing-content.md#edit-component-layout)

   * Utilizzando l’opzione **Layout** nel menu Azioni rapide del componente è possibile passare alla modalità **Layout**.
   * La modalità **Layout** persiste quando si modifica il componente e torna alla modalità **Modifica** quando è attivo un altro componente.

In modalità Layout puoi eseguire diverse azioni su una griglia:

* Ridimensionare i componenti di contenuto utilizzando i punti blu. Il ridimensionamento sarà sempre con ancoraggio sulla griglia. Quando si esegue un’operazione di ridimensionamento, verrà visualizzata la griglia di sfondo per facilitare l’allineamento:

   ![screen_shot_2018-03-23at090140](assets/screen_shot_2018-03-23at090140.png)

   >[!NOTE]
   >
   >Proporzioni e rapporti relativi saranno mantenuti al ridimensionamento di componenti come le **immagini**.

* Facendo clic/toccando un componente di contenuti la barra degli strumenti consente di:

   * **Elemento padre**

      Consente di selezionare l’intero componente Contenitore di layout per intervenire su di esso nel complesso.

   * **Mobile in nuova riga**

      Il componente viene spostato su una nuova riga, a seconda dello spazio disponibile all’interno della griglia.

   * **Nascondi componente**

      Il componente viene reso invisibile (può essere ripristinato dalla barra degli strumenti del Contenitore di layout).
   ![screen_shot_2018-03-23at090246](assets/screen_shot_2018-03-23at090246.png)

* In modalità **Layout** tocca o fai clic su **Trascina qui i componenti** per selezionare l’intero componente. Viene quindi visualizzata la barra degli strumenti per questa modalità.

   La barra degli strumenti presenta opzioni diverse a seconda dello stato del componente del layout e dei componenti che ne fanno parte. Esempio:

   * **Elemento padre:** consente di selezionare il componente principale.

   ![](do-not-localize/screen_shot_2018-03-23at090823.png)

   * **Mostra componenti nascosti** - Mostra tutti i componenti o singoli componenti. Il numero indica quanti sono attualmente i componenti nascosti.Il contatore mostra quanti sono i componenti nascosti.

   ![](do-not-localize/screen_shot_2018-03-23at091007.png)

   * **Ripristina layout punto di interruzione**: consente di tornare al layout predefinito e non verrà quindi applicato alcun layout personalizzato.

   ![](do-not-localize/screen_shot_2018-03-23at091013.png)

   * **Mobile in nuova riga:** consente di alzare il componente di una posizione, se lo spazio è sufficiente.

   ![screen_shot_2018-03-23at090829](assets/screen_shot_2018-03-23at090829.png)

   * **Nascondi componente:** consente di nascondere il componente corrente.

   ![](do-not-localize/screen_shot_2018-03-23at090834.png)

   >[!NOTE]
   >
   >Nell’esempio in alto le azioni Mobile e Nascondi sono disponibili, perché questo Contenitore di layout è nidificato all’interno di un Contenitore di layout principale.

   * **Rivela componenti**
Seleziona i componenti principali per visualizzare la barra degli strumenti delle azioni con 
l’opzione **Mostra componenti nascosti**. In questo esempio, due componenti sono nascosti.
   ![screen_shot_2018-03-23at091200](assets/screen_shot_2018-03-23at091200.png)

   Selezionando l’opzione **Mostra componenti nascosti**, i componenti che sono attualmente nascosti nelle posizioni originali vengono visualizzati in blu.

   ![screen_shot_2018-03-23at091224](assets/screen_shot_2018-03-23at091224.png)

   Selezionando **Ripristina tutto**, tutti i componenti nascosti diventano visibili.
