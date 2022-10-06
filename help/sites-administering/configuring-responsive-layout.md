---
title: Configurazione del contenitore di layout e della modalità di layout
seo-title: Configuring Layout Container and Layout Mode
description: Scopri come configurare il Contenitore di layout e la Modalità di layout.
seo-description: Learn how to configure Layout Container and Layout Mode.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 8%

---

# Configurazione del contenitore di layout e della modalità di layout{#configuring-layout-container-and-layout-mode}

[Layout reattivo](/help/sites-authoring/responsive-layout.md) è un meccanismo di realizzazione [web design dinamico](https://en.wikipedia.org/wiki/Responsive_web_design). Questo consente all’utente di creare pagine web con layout e dimensioni che dipendono dai dispositivi utilizzati dagli utenti.

>[!NOTE]
>
>Questo può essere confrontato con il [Web per dispositivi mobili](/help/sites-developing/mobile-web.md) che utilizzano web design adattivo (principalmente per l’interfaccia classica).

AEM consente di realizzare il layout dinamico per le pagine utilizzando una combinazione di meccanismi:

* Componente [**Contenitore di layout**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)

   Questo componente fornisce un sistema paragrafo a griglia che consente di aggiungere e posizionare i componenti all’interno di una griglia reattiva. Può essere utilizzato come parsys predefinito per la pagina e/o reso disponibile agli autori nel browser Componenti.

   * Il valore predefinito **Contenitore di layout** il componente è definito in:

      /libs/wcm/foundation/components/responsivegrid

   * Puoi definire contenitori layout:

      * Componente che l’utente può aggiungere a una pagina.
      * Come impostazione predefinita parsys per la pagina.
      * Entrambe.

         È possibile avere il Contenitore di layout come standard per la pagina, consentendo all’utente di aggiungere altri contenitori di layout al suo interno; ad esempio, per ottenere il controllo delle colonne.

* **[Modalità Layout](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
Una volta che il Contenitore di layout è collocato nella pagina, è possibile utilizzare la funzione 
**Layout** per posizionare il contenuto all’interno della griglia reattiva.

* [**Emulatore**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate) Consente di creare e modificare siti Web reattivi il cui layout si riorganizza in base alle dimensioni del dispositivo/finestra, ridimensionando i componenti in modo interattivo. L’utente può quindi visualizzare quale sarà l’aspetto dei contenuti utilizzando l’emulatore.

>[!CAUTION]
>
>Anche se la **Contenitore di layout** Il componente è disponibile nell’interfaccia classica, le sue funzionalità complete sono disponibili solo nell’interfaccia touch.

Con questi meccanismi basati su una griglia reattiva è possibile:

* Utilizza i punti di interruzione (che indicano il raggruppamento dei dispositivi) per definire comportamenti di contenuto diversi in base al layout del dispositivo.
* Nascondere i componenti in base al gruppo di dispositivi (definire il punto di interruzione che un componente deve nascondere).
* Utilizzare l&#39;ancoraggio orizzontale sulla griglia (posizionare i componenti sulla griglia, ridimensionarli come necessario, definire quando dovrebbero venire compressi/ridisposti in modo da essere affiancati o sovrapposti).
* Gestire il controllo delle colonne.

>[!NOTE]
>
>In un’installazione standard, è stato configurato il layout dinamico per [Sito di riferimento We.Retail](/help/sites-developing/we-retail.md). Lei deve ancora [attivare il componente Contenitore di layout](#enable-the-layout-container-component-for-page) per altre pagine.

## Configurazione dell’emulatore reattivo {#configuring-the-responsive-emulator}

Queste attività ti consentono di visualizzare il reattivo **Emulatore** sul tuo sito.

### Registra i componenti pagina per emulazione {#register-your-page-components-for-emulation}

Per abilitare l’emulatore a supportare le pagine, è necessario registrare i componenti della pagina. Vedi [Registrazione dei componenti della pagina per la simulazione](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### Specificare i gruppi di dispositivi {#specify-the-device-groups}

Per specificare i gruppi di dispositivi visualizzati nell&#39;elenco Dispositivi dell&#39;emulatore, vedi [Specifica dei gruppi di dispositivi](/help/sites-developing/responsive.md#specifying-the-device-groups).

### Collegare il sito ai gruppi di dispositivi specificati {#link-your-site-to-the-specified-device-groups}

Per includere l&#39;emulatore è necessario collegare il sito ai gruppi di dispositivi. Vedi [Aggiunta dell’elenco dei dispositivi](/help/sites-developing/responsive.md#adding-the-devices-list) (sia per l’interfaccia classica che per quella touch).

## Attiva la modalità Layout per il sito {#activate-layout-mode-for-your-site}

Tali procedure sono utilizzate per **Layout** sul sito.

### Configurare i punti di interruzione {#configure-the-breakpoints}

[Punti di interruzione](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* Sono utilizzati nel design reattivo.
* Può essere definito:

   * Nel modello di pagina, da dove le impostazioni verranno copiate in tutte le pagine create con tale modello.
   * Sul nodo della pagina, da dove le impostazioni verranno ereditate da qualsiasi pagina figlia.

* Definire un titolo e una larghezza:

   * Il titolo descrive il raggruppamento di dispositivi generico, con orientamento se necessario; ad esempio telefono, tablet, tablet.
   * La larghezza definisce la larghezza massima in pixel per quel raggruppamento di dispositivi generico. Ad esempio, se il telefono punto di interruzione ha una larghezza di 768, la larghezza massima del layout utilizzato per un dispositivo telefonico.

* Sono visibili come marcatori nella parte superiore dell’editor di pagine quando utilizzi l’emulatore.
* Sono ereditate dalla gerarchia dei nodi principali e possono essere ignorate a piacimento.
* È disponibile un punto di interruzione predefinito (preconfigurato) che copre tutto quanto si trova al di sopra dell’ultimo *configurato* punto di interruzione.

È possibile definirli utilizzando CRXDE Lite o XML.

>[!NOTE]
>
>Se stai impostando un nuovo progetto:
>
>* è necessario aggiungere punti di interruzione ai modelli.
>
>Se stai eseguendo la migrazione di un progetto esistente (con contenuto esistente), devi:
>
>* aggiungere punti di interruzione ai modelli
>* aggiungere gli stessi punti di interruzione alle pagine esistenti
>
>  Poiché l’ereditarietà è attiva, puoi limitarla alla pagina principale del contenuto.

#### Configurazione dei punti di interruzione con CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Utilizzando CRXDE Lite (o equivalente), accedi a:

   * Definizione del modello.
   * La `jcr:content` nodo della pagina.

1. Sotto `jcr:content` crea il nodo:

   * Nome: `cq:responsive`
   * Tipo: `nt:unstructured`

1. Sotto questo crea il nodo:

   * Nome: `breakpoints`
   * Tipo: `nt:unstructured`

1. Sotto il nodo dei punti di interruzione è possibile creare un numero qualsiasi di punti di interruzione. Ogni definizione è un singolo nodo con le seguenti proprietà:

   * Nome: `<descriptive name>`
   * Tipo: `nt:unstructured`
   * Titolo: `String` * `<descriptive title seen in Emulator>`*
   * Larghezza: `Decimal` * `<value of breakpoint>`*

#### Configurazione dei punti di interruzione tramite XML {#configuring-breakpoints-using-xml}

I punti di interruzione si trovano all’interno della `<jcr:content>` della sezione `.context.html` nella cartella del modello (o contenuto) appropriata.

Una definizione di esempio:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### Aggiungere un provider di informazioni reattive {#add-a-responsive-information-provider}

>[!NOTE]
>
>Questa opzione è necessaria solo se il componente della pagina non è basato sul componente della pagina di base.

Copia quanto segue `cq:infoProviders` struttura del nodo nel componente della pagina padre:

`/libs/foundation/components/page/cq:infoProviders/responsive`

## Abilita ridimensionamento componente per la pagina {#enable-component-resizing-for-the-page}

Queste procedure sono necessarie per ridimensionare i componenti nel **Layout** modalità.

### Imposta contenitore di layout come parsys principale {#set-layout-container-as-main-parsys}

Per impostare parsys principale della pagina come contenitore di layout, è necessario definire parsys come segue:

`wcm/foundation/components/responsivegrid`

In:

* Componente pagina
* Modello di pagina (per utilizzi futuri)

I due esempi seguenti illustrano la definizione:

* **HTL:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP:**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### Includere i CSS reattivi {#include-the-responsive-css}

#### CSS per punti di interruzione con LESS {#css-for-breakpoints-using-less}

AEM utilizza LESS per generare parti del CSS necessario, queste devono essere incluse nei progetti.

Sarà inoltre necessario creare un [libreria client](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html) per fornire ulteriori chiamate di configurazione e di funzione. Il seguente estratto di LESS è un esempio del minimo da aggiungere al progetto:

```java
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

La definizione della griglia di base si trova in:

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### Considerazioni sullo stile {#styling-considerations}

I componenti contenuti in un contenitore dinamico vengono ridimensionati (insieme ai rispettivi elementi DOM di HTML) in base alle dimensioni della griglia reattiva. Pertanto, in queste circostanze, si raccomanda di evitare (o aggiornare) le definizioni di elementi DOM a larghezza fissa (contenuti).

Esempio:

* Prima:

   * `width=100px`

* Dopo:

   * `max-width=100px`

#### Ridimensionamento e conformità alle immagini adattive {#resizing-and-adaptive-image-compliance}

Qualsiasi ridimensionamento di un componente all’interno della griglia attiverà i seguenti ascoltatori:

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

Per ridimensionare e aggiornare correttamente il contenuto di un’immagine adattiva inclusa in una griglia reattiva, è necessario aggiungere un `afterEdit` impostato su `REFRESH_PAGE` nel `EditConfig` file di ogni componente contenuto.

Esempio:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

Il meccanismo di immagine adattiva è reso disponibile tramite uno script che controlla la selezione dell&#39;immagine corretta per le dimensioni correnti della finestra. Si attiva dopo che il DOM è pronto o quando riceve un evento dedicato. Al momento la pagina deve essere aggiornata per riflettere correttamente il risultato dell’azione dell’utente.

>[!CAUTION]
>
>Le clientlibs personalizzate del foglio di stile devono essere caricate come parte dell’intestazione affinché funzionino correttamente sia su autore che su pubblicazione.

## Abilita il componente Contenitore di layout per pagina {#enable-the-layout-container-component-for-page}

Queste attività consentono agli autori di trascinare le istanze della **Contenitore di layout** nella pagina.

### Attivare il componente Contenitore di layout per la modifica delle pagine {#enable-the-layout-container-component-for-page-editing}

Per consentire agli autori di aggiungere ulteriori griglie reattive alle pagine di contenuto, è necessario abilitare il componente Contenitore di layout per la pagina. Puoi eseguire questa operazione utilizzando:

* **Ambiente di authoring**

   Utilizzo [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md) per attivare **Contenitore livello** per una pagina.

* **Definizione del componente**

   Utilizzo `allowedComponent` o un’inclusione statica durante la definizione del componente.

### Configurare la griglia del contenitore di layout {#configure-the-grid-of-the-layout-container}

Puoi configurare il numero di colonne disponibili per ogni istanza specifica del contenitore di layout:

1. **Ambiente di authoring**

   È possibile configurare il numero di colonne disponibili per ogni istanza specifica del contenitore di layout.

   A questo scopo, utilizza [Modalità Progettazione](/help/sites-authoring/default-components-designmode.md), quindi apri la finestra di dialogo di progettazione per il contenitore richiesto. Qui puoi specificare quante colonne saranno disponibili per il posizionamento e il dimensionamento. Il valore predefinito è 12.

1. **XML**

   Le definizioni della griglia dinamica sono specificate in:

   `etc/design/<*your-project-name*>/.content.xml`

   È possibile definire i seguenti parametri:

   * Numero di colonne disponibili:

      * `columns="{String}8"`
   * Componenti che possono essere aggiunti al componente corrente:

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
