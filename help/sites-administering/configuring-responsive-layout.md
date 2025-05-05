---
title: Configurazione del contenitore di layout e della modalità layout
description: Scopri come configurare Contenitore di layout e Modalità di layout.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 17c4084d9ee93e5fe6652d63438eaf34cbc83c12
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 2%

---


# Configurazione del contenitore di layout e della modalità layout{#configuring-layout-container-and-layout-mode}

Scopri come configurare Contenitore di layout e Modalità di layout.

>[!TIP]
>
>Questo documento fornisce una panoramica della progettazione reattiva per amministratori e sviluppatori del sito e descrive come vengono realizzate le funzioni nell’AEM.
>
>Per gli autori di contenuto, i dettagli sull&#39;utilizzo delle funzionalità di progettazione reattiva in una pagina di contenuto sono disponibili nel documento [Layout reattivo per le pagine di contenuto.](/help/sites-authoring/responsive-layout.md)

## Panoramica {#overview}

[Layout reattivo](/help/sites-authoring/responsive-layout.md) è un meccanismo per la realizzazione di [design responsive](https://en.wikipedia.org/wiki/Responsive_web_design). Questo consente all’utente di creare pagine web con un layout e dimensioni che dipendono dai dispositivi utilizzati dagli utenti.

AEM consente di realizzare il layout dinamico per le pagine utilizzando una combinazione di meccanismi:

* Componente [**Contenitore di layout**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)

  Questo componente fornisce un sistema paragrafo a griglia che consente di aggiungere e posizionare i componenti all’interno di una griglia reattiva. Può essere utilizzato come parsys predefinito per la pagina e/o reso disponibile agli autori nel browser componenti.

   * Il componente predefinito **Contenitore di layout** è definito in:

     `/libs/wcm/foundation/components/responsivegrid`

   * Puoi definire i contenitori di layout:

      * Come componente che l’utente può aggiungere a una pagina.
      * Come parsys predefinito per la pagina.
      * Entrambi.

        Puoi avere il contenitore di layout come standard per la pagina, consentendo allo stesso tempo all’utente di aggiungere ulteriori contenitori di layout all’interno di questo; ad esempio, per ottenere il controllo delle colonne.

* **[Modalità Layout](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
Una volta che il contenitore di layout è posizionato nella pagina, è possibile utilizzare la modalità **Layout** per posizionare il contenuto all&#39;interno della griglia reattiva.

* [**Emulatore**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
Questo consente di creare e modificare siti web dinamici il cui layout si riorganizza in base alle dimensioni del dispositivo o della finestra, ridimensionando i componenti in modo interattivo. L’utente può quindi visualizzare come viene eseguito il rendering del contenuto utilizzando l’emulatore.

Con questi meccanismi basati su una griglia dinamica è possibile:

* Utilizza i punti di interruzione (che indicano il raggruppamento del dispositivo) per definire un comportamento di contenuto diverso in base al layout del dispositivo.
* Nascondi i componenti in base al gruppo di dispositivi (definisci il punto di interruzione in cui un componente verrà nascosto).
* Utilizzate l&#39;aggancio orizzontale alla griglia (posizionate i componenti nella griglia, ridimensionate secondo necessità, definite quando comprimerli o rifluirli per essere affiancati o superiori/inferiori).
* Gestire il controllo delle colonne.

>[!TIP]
>
>Adobe fornisce la [documentazione GitHub](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) del layout reattivo come riferimento per gli sviluppatori front-end, consentendo loro di utilizzare la griglia AEM al di fuori dell&#39;AEM, ad esempio, durante la creazione di modelli statici di HTML per un futuro sito AEM.

>[!NOTE]
>
>In un&#39;installazione predefinita, il layout dinamico è stato configurato per il [sito di riferimento We.Retail](/help/sites-developing/we-retail.md). [Attiva il componente Contenitore di layout](#enable-the-layout-container-component-for-page) per altre pagine.

>[!CAUTION]
>
>Sebbene il componente **Contenitore di layout** sia disponibile nell&#39;interfaccia utente classica, la sua funzionalità completa è disponibile solo nell&#39;interfaccia touch.

## Configurazione dell’emulatore reattivo {#configuring-the-responsive-emulator}

Questa attività ti consente di visualizzare l&#39;**emulatore** reattivo sul tuo sito.

### Registrare i componenti pagina per l’emulazione {#register-your-page-components-for-emulation}

Per abilitare l’emulatore a supportare le pagine, è necessario registrare i componenti della pagina. Consulta [Registrazione dei componenti pagina per la simulazione](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### Specificare i gruppi di dispositivi {#specify-the-device-groups}

Per specificare i gruppi di dispositivi visualizzati nell&#39;elenco Dispositivi dell&#39;emulatore, vedere [Specifica dei gruppi di dispositivi](/help/sites-developing/responsive.md#specifying-the-device-groups).

### Collega il sito ai gruppi di dispositivi specificati {#link-your-site-to-the-specified-device-groups}

Per includere l’emulatore, collega il sito ai gruppi di dispositivi. Consulta [Aggiunta dell&#39;elenco dei dispositivi](/help/sites-developing/responsive.md#adding-the-devices-list) (sia per l&#39;interfaccia utente classica che per quella ottimizzata per il tocco).

## Attiva modalità layout per il sito {#activate-layout-mode-for-your-site}

Queste procedure vengono utilizzate per attivare la modalità **Layout** nel sito.

### Configurare i punti di interruzione {#configure-the-breakpoints}

[Punti di interruzione](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* Sono utilizzati nella progettazione reattiva.
* Può essere definito:

   * Nel modello della pagina, da dove le impostazioni vengono copiate nelle pagine create con tale modello.
   * Nel nodo della pagina, da dove le impostazioni vengono ereditate da eventuali pagine figlie.

* Definisci un titolo e una larghezza:

   * Il titolo descrive il raggruppamento generico del dispositivo, con orientamento se necessario; ad esempio telefono, tablet, tabletorizzontale.
   * La larghezza definisce la larghezza massima in pixel per il raggruppamento di dispositivi generico. Ad esempio, se il telefono del punto di interruzione ha una larghezza di 768, deve corrispondere alla larghezza massima del layout utilizzato per un dispositivo telefonico.

* Sono visibili come marcatori nella parte superiore dell’editor pagina quando utilizzi l’emulatore.
* Sono ereditati dalla gerarchia dei nodi principali e possono essere sostituiti a piacimento.
* Esiste un punto di interruzione predefinito che copre tutto ciò che si trova oltre l&#39;ultimo punto di interruzione *configurato*.

Possono essere definiti utilizzando CRXDE Lite o XML.

>[!NOTE]
>
>Se stai impostando un nuovo progetto:
>
>* aggiungi punti di interruzione ai modelli.
>
>Se stai eseguendo la migrazione di un progetto esistente (con contenuto esistente), devi:
>
>* aggiungere punti di interruzione ai modelli
>* aggiungere gli stessi punti di interruzione alle pagine esistenti
>
>  Quando l’ereditarietà è in funzione, puoi limitarla alla pagina principale del contenuto.

#### Configurazione dei punti di interruzione tramite CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Utilizzando CRXDE Lite (o equivalente), accedi a:

   * Definizione del modello.
   * Il nodo `jcr:content` della pagina.

1. In `jcr:content` creare il nodo:

   * Nome: `cq:responsive`
   * Tipo: `nt:unstructured`

1. In questo caso, crea il nodo:

   * Nome: `breakpoints`
   * Tipo: `nt:unstructured`

1. Nel nodo dei punti di interruzione è possibile creare un numero qualsiasi di punti di interruzione. Ogni definizione è un singolo nodo con le seguenti proprietà:

   * Nome: `<descriptive name>`
   * Tipo: `nt:unstructured`
   * Titolo: `String` * `<descriptive title seen in Emulator>`*
   * Larghezza: `Decimal` * `<value of breakpoint>`*

#### Configurazione dei punti di interruzione tramite XML {#configuring-breakpoints-using-xml}

I punti di interruzione si trovano all&#39;interno della sezione `<jcr:content>` di `.context.html` nella cartella del modello (o del contenuto) appropriata.

Esempio di definizione:

```html
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### Aggiungere un provider di informazioni reattivo {#add-a-responsive-information-provider}

>[!NOTE]
>
>Questa opzione è necessaria solo se il componente Pagina non è basato sul componente Pagina di base.

Copia la seguente struttura di nodi `cq:infoProviders` nel componente della pagina padre:

`/libs/foundation/components/page/cq:infoProviders/responsive`

## Abilita il ridimensionamento dei componenti per la pagina {#enable-component-resizing-for-the-page}

Queste procedure sono necessarie per ridimensionare i componenti in modalità **Layout**.

### Imposta contenitore layout come parsys principale {#set-layout-container-as-main-parsys}

Per impostare il parsys principale della pagina come contenitore di layout, definisci il parsys come:

`wcm/foundation/components/responsivegrid`

In:

* Componente pagina
* Modello pagina (per utilizzi futuri)

I due esempi seguenti illustrano la definizione:

* **HTL:**

  ```html
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP:**

  ```html
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### Includi CSS reattivo {#include-the-responsive-css}

#### CSS per i punti di interruzione che utilizzano MENO {#css-for-breakpoints-using-less}

AEM utilizza LESS per generare parti del CSS necessario, che devono essere incluse nei progetti.

Sarà inoltre necessario creare una [libreria client](https://experienceleague.adobe.com/docs/?lang=it) per fornire ulteriori chiamate di configurazione e funzione. Il seguente estratto LESS è un esempio del minimo da aggiungere al progetto:

```css
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

La definizione della griglia di base è disponibile in:

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### Considerazioni sullo stile {#styling-considerations}

I componenti contenuti in un contenitore reattivo vengono ridimensionati (insieme ai rispettivi elementi DOM HTML) in base alla dimensione della griglia reattiva. Pertanto, in queste circostanze, si consiglia di evitare (o aggiornare) le definizioni degli elementi DOM a larghezza fissa (contenuti).

Ad esempio:

* Prima:

   * `width=100px`

* Dopo:

   * `max-width=100px`

#### Ridimensionamento e conformità dell&#39;immagine adattiva {#resizing-and-adaptive-image-compliance}

Qualsiasi ridimensionamento di un componente all’interno della griglia attiva i seguenti listener, a seconda delle necessità:

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

Per ridimensionare e aggiornare correttamente il contenuto di un&#39;immagine adattiva inclusa in una griglia reattiva, è necessario aggiungere un set `afterEdit` al listener `REFRESH_PAGE` nel file `EditConfig` di ogni componente contenuto.

Ad esempio:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

Il meccanismo di immagine adattiva è reso disponibile tramite uno script che controlla la selezione dell’immagine corretta per le dimensioni correnti della finestra. Si attiva dopo che il DOM è pronto o quando si riceve un evento dedicato. Attualmente è necessario aggiornare la pagina per riflettere correttamente il risultato dell’azione dell’utente.

>[!CAUTION]
>
>Le clientlibs dei fogli di stile personalizzati devono essere caricate come parte dell’intestazione affinché funzionino correttamente durante l’authoring e la pubblicazione.

## Abilitare il componente Contenitore di layout per la pagina {#enable-the-layout-container-component-for-page}

Queste attività consentono agli autori di trascinare nella pagina le istanze del componente **Contenitore di layout**.

### Abilitare il componente Contenitore di layout per la modifica delle pagine {#enable-the-layout-container-component-for-page-editing}

Per consentire agli autori di aggiungere ulteriori griglie reattive alle pagine di contenuto, devi abilitare il componente Contenitore di layout per la pagina. Puoi eseguire questa operazione utilizzando:

* **Ambiente di authoring**

  Utilizza la [modalità progettazione](/help/sites-authoring/default-components-designmode.md) per attivare il componente **Contenitore livello** per una pagina.

* **Definizione componente**

  Usa `allowedComponent` o un&#39;inclusione statica durante la definizione del componente.

### Configurare la griglia del contenitore di layout {#configure-the-grid-of-the-layout-container}

Puoi configurare il numero di colonne disponibili per ogni istanza specifica del contenitore di layout:

1. **Ambiente di authoring**

   Puoi configurare il numero di colonne disponibili per ogni istanza specifica del contenitore di layout.

   A tale scopo, utilizzare [Modalità progettazione](/help/sites-authoring/default-components-designmode.md), quindi aprire la finestra di dialogo per la progettazione del contenitore richiesto. Qui puoi specificare quante colonne saranno disponibili per il posizionamento e il dimensionamento. Il valore predefinito è 12.

1. **XML**

   Le definizioni per la griglia reattiva sono specificate in:

   `etc/design/<*your-project-name*>/.content.xml`

   È possibile definire i seguenti parametri:

   * Numero di colonne disponibili:

      * `columns="{String}8"`

   * Componenti che possono essere aggiunti al componente corrente:

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`

## Griglie reattive nidificate {#nested-responsive-grids}

In alcuni casi potrebbe essere necessario nidificare le griglie reattive per supportare le esigenze del progetto. Tuttavia, tieni presente che la best practice consigliata da Adobe è quella di mantenere la struttura il più piatto possibile.

Quando non puoi evitare di utilizzare griglie reattive nidificate, assicurati che:

* Tutti i contenitori (contenitori, schede, fisarmoniche, ecc.) hanno la proprietà `layout = responsiveGrid`.
* Non combinare la proprietà `layout = simple` nella gerarchia dei contenitori.

Sono inclusi tutti i contenitori strutturali del modello della pagina.

Il numero di colonna del contenitore interno non deve mai essere maggiore di quello del contenitore esterno. L&#39;esempio seguente soddisfa questa condizione. Mentre il numero di colonna del contenitore esterno è 8 per la schermata predefinita (desktop), il numero di colonna del contenitore interno è 4.

>[!BEGINTABS]

>[!TAB Esempio di struttura del nodo]

```text
container
  @layout = responsiveGrid
  cq:responsive
    default
      @offset = 0
      @width = 8
  container
  @layout = responsiveGrid
    cq:responsive
      default
        @offset = 0
        @width = 4
    text
      @text =" Text Column 1"
```

>[!TAB Esempio di HTML risultante]

```html
<div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--default--8 aem-GridColumn--offset--default--0">
  <div id="container-c9955c233c" class="cmp-container">
    <div class="aem-Grid aem-Grid--8 aem-Grid--default--8 ">
      <div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--offset--default--0 aem-GridColumn--default--4">
        <div id="container-8414e95866" class="cmp-container">
          <div class="aem-Grid aem-Grid--4 aem-Grid--default--4 ">
            <div class="text aem-GridColumn aem-GridColumn--default--4">
              <div data-cmp-data-layer="..." id="text-1234567890" class="cmp-text">
                <p>Text Column 1</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

>[!ENDTABS]
