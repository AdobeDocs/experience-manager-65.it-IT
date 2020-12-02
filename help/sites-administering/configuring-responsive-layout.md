---
title: Configurazione del Contenitore di layout e della modalità Layout
seo-title: Configurazione del Contenitore di layout e della modalità Layout
description: Scoprite come configurare il Contenitore di layout e la modalità Layout.
seo-description: Scoprite come configurare il Contenitore di layout e la modalità Layout.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 8%

---


# Configurazione del Contenitore di layout e della modalità Layout{#configuring-layout-container-and-layout-mode}

[Layout reattivo ](/help/sites-authoring/responsive-layout.md) è un meccanismo per realizzare un design [ Web ](https://en.wikipedia.org/wiki/Responsive_web_design)reattivo. Questo consente all&#39;utente di creare pagine Web con layout e dimensioni dipendenti dai dispositivi utilizzati dagli utenti.

>[!NOTE]
>
>Questo può essere confrontato con i meccanismi [Mobile Web](/help/sites-developing/mobile-web.md), che utilizzano la progettazione Web adattiva (principalmente per l&#39;interfaccia classica).

AEM consente di realizzare il layout dinamico per le pagine utilizzando una combinazione di meccanismi:

* Componente [**Contenitore di layout**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)

   Questo componente fornisce un sistema paragrafo a griglia che consente di aggiungere e posizionare componenti all’interno di una griglia reattiva. Può essere usato come parsys predefinito per la pagina e/o reso disponibile agli autori nel browser dei componenti.

   * Il componente predefinito **Contenitore di layout** è definito in:

      /libs/wcm/foundation/components/responsivegrid

   * È possibile definire contenitori di layout:

      * Componente che l’utente può aggiungere a una pagina.
      * Come impostazione predefinita parsys per la pagina.
      * Entrambe.

         Potete avere il Contenitore di layout come standard per la pagina, consentendo all&#39;utente di aggiungere altri contenitori di layout all&#39;interno di questo; ad esempio, per ottenere il controllo delle colonne.

* **[Modalità](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
LayoutUna volta che il Contenitore di layout è posizionato sulla pagina, è possibile utilizzare la 
**Modalità** Layout per posizionare il contenuto all&#39;interno della griglia reattiva.

* [**Emulatore**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate) Consente di creare e modificare siti Web reattivi il cui layout si riorganizza in base alle dimensioni del dispositivo/finestra, ridimensionando i componenti in modo interattivo. L’utente può quindi visualizzare quale sarà l’aspetto dei contenuti utilizzando l’emulatore.

>[!CAUTION]
>
>Anche se il componente **Contenitore di layout** è disponibile nell&#39;interfaccia classica, le sue funzionalità complete sono disponibili solo nell&#39;interfaccia touch.

Con questi meccanismi basati su una griglia reattiva è possibile:

* Usate punti di interruzione (che indicano il raggruppamento dei dispositivi) per definire comportamenti di contenuto diversi in base al layout del dispositivo.
* Nascondere i componenti in base al gruppo di dispositivi (definire il punto di interruzione che un componente deve nascondere).
* Utilizzare l&#39;ancoraggio orizzontale sulla griglia (posizionare i componenti sulla griglia, ridimensionarli come necessario, definire quando dovrebbero venire compressi/ridisposti in modo da essere affiancati o sovrapposti).
* Gestire il controllo delle colonne.

>[!NOTE]
>
>In un&#39;installazione out-of-the-box, il layout reattivo è stato configurato per il [sito di riferimento We.Retail](/help/sites-developing/we-retail.md). È comunque necessario attivare il componente Contenitore di layout [per altre pagine.](#enable-the-layout-container-component-for-page)

## Configurazione dell&#39;emulatore reattivo {#configuring-the-responsive-emulator}

Queste attività consentono di visualizzare sul sito l&#39;emulatore reattivo **Emulatore**.

### Registra i componenti della pagina per l&#39;emulazione {#register-your-page-components-for-emulation}

Per consentire all’emulatore di supportare le pagine, è necessario registrare i componenti della pagina. Vedere [Registrazione di componenti di pagina per la simulazione](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### Specificare i gruppi di dispositivi {#specify-the-device-groups}

Per specificare i gruppi di dispositivi che vengono visualizzati nell&#39;elenco Dispositivi dell&#39;emulatore, vedere [Specifica dei gruppi di dispositivi](/help/sites-developing/responsive.md#specifying-the-device-groups).

### Collegate il sito ai gruppi di dispositivi specificati {#link-your-site-to-the-specified-device-groups}

Per includere l&#39;emulatore è necessario collegare il sito ai gruppi di dispositivi. Consultate [Aggiunta dell&#39;elenco dei dispositivi](/help/sites-developing/responsive.md#adding-the-devices-list) (per entrambe le interfacce, sia classica che touch).

## Attivare la modalità Layout per il sito {#activate-layout-mode-for-your-site}

Queste procedure vengono utilizzate per attivare la modalità **Layout** sul sito.

### Configurare i punti di interruzione {#configure-the-breakpoints}

[Punti di interruzione](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* Sono utilizzati nel design reattivo.
* Può essere definito:

   * Nel modello di pagina, le impostazioni verranno copiate nelle pagine create con tale modello.
   * Sul nodo della pagina, da cui le impostazioni verranno ereditate da qualsiasi pagina figlia.

* Definire un titolo e una larghezza:

   * Il titolo descrive il raggruppamento di dispositivi generico, con orientamento, se necessario; ad esempio telefono, tablet, tablet.
   * La larghezza definisce la larghezza massima in pixel per il raggruppamento di dispositivi generico. Ad esempio, se il telefono punto di interruzione ha una larghezza di 768, la larghezza massima del layout utilizzato per un dispositivo telefonico è pari a 768.

* Sono visibili come marcatori nella parte superiore dell’editor di pagina quando si utilizza l’emulatore.
* Sono ereditate dalla gerarchia dei nodi padre e possono essere sostituite a piacimento.
* Esiste un punto di interruzione predefinito (out-of-the-box) che copre tutto quanto si trova sopra l&#39;ultimo punto di interruzione *configurato*.

Possono essere definiti utilizzando CRXDE Lite o XML.

>[!NOTE]
>
>Se state configurando un nuovo progetto:
>
>* è necessario aggiungere punti di interruzione ai modelli.
>
>
Se state eseguendo la migrazione di un progetto esistente (con contenuto esistente), dovete:
>
>* aggiungere punti di interruzione ai modelli
>* aggiungere gli stessi punti di interruzione alle pagine esistenti

>
>  
Poiché l’ereditarietà è attiva, potete limitare questa opzione alla pagina principale del contenuto.

#### Configurazione dei punti di interruzione con CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. Utilizzando CRXDE Lite (o equivalente), andate a:

   * Definizione del modello.
   * Il nodo `jcr:content` della pagina.

1. In `jcr:content` creare il nodo:

   * Nome: `cq:responsive`
   * Tipo: `nt:unstructured`

1. In questa sezione creare il nodo:

   * Nome: `breakpoints`
   * Tipo: `nt:unstructured`

1. Sotto il nodo punti di interruzione è possibile creare un numero qualsiasi di punti di interruzione. Ogni definizione è un nodo singolo con le seguenti proprietà:

   * Nome: `<descriptive name>`
   * Tipo: `nt:unstructured`
   * Titolo: `String` * `<descriptive title seen in Emulator>`*
   * Larghezza: `Decimal` * `<value of breakpoint>`*

#### Configurazione dei punti di interruzione con XML {#configuring-breakpoints-using-xml}

I punti di interruzione si trovano all&#39;interno della sezione `<jcr:content>` della cartella `.context.html` nella cartella del modello (o del contenuto) appropriata.

Definizione di esempio:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### Aggiunta di un provider di informazioni reattive {#add-a-responsive-information-provider}

>[!NOTE]
>
>Questo è necessario solo se il componente pagina non è basato sul componente pagina di base.

Copiate la seguente struttura di nodi `cq:infoProviders` nel componente della pagina padre:

`/libs/foundation/components/page/cq:infoProviders/responsive`

## Abilita ridimensionamento componenti per la pagina {#enable-component-resizing-for-the-page}

Queste procedure sono necessarie per ridimensionare i componenti nella modalità **Layout**.

### Imposta Contenitore di layout come parsys principale {#set-layout-container-as-main-parsys}

Per impostare parsys principale della pagina come contenitore di layout, è necessario definire parsys come:

`wcm/foundation/components/responsivegrid`

In:

* Componente pagina
* Modello di pagina (per uso futuro)

I due esempi seguenti illustrano la definizione:

* **HTL:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP:**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### Includere il CSS reattivo {#include-the-responsive-css}

#### CSS per punti di interruzione con LESS {#css-for-breakpoints-using-less}

AEM utilizza LESS per generare parti del CSS necessario, che devono essere incluse nei progetti.

Sarà inoltre necessario creare una [libreria client](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html) per fornire ulteriori chiamate di configurazione e funzioni. Il seguente estratto LESS è un esempio del minimo da aggiungere al progetto:

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

I componenti contenuti in un contenitore reattivo verranno ridimensionati (insieme ai rispettivi elementi DOM HTML) in base alle dimensioni della griglia reattiva. Pertanto, in queste circostanze, si consiglia di evitare (o aggiornare) le definizioni di elementi DOM a larghezza fissa (contenuti).

Esempio:

* Prima:

   * `width=100px`

* Dopo:

   * `max-width=100px`

#### Ridimensionamento e conformità dell&#39;immagine adattiva {#resizing-and-adaptive-image-compliance}

Qualsiasi ridimensionamento di un componente all&#39;interno della griglia attiverà i seguenti listener:

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

Per ridimensionare e aggiornare correttamente il contenuto di un&#39;immagine adattiva inclusa in una griglia reattiva, è necessario aggiungere un `afterEdit` impostato su `REFRESH_PAGE` listener nel file `EditConfig` di ogni componente contenuto.

Esempio:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

Il meccanismo di immagine adattiva è reso disponibile tramite uno script che controlla la selezione dell&#39;immagine corretta per le dimensioni correnti della finestra. Viene attivato dopo che il DOM è pronto o quando riceve un evento dedicato. Al momento la pagina deve essere aggiornata per riflettere correttamente il risultato dell&#39;azione dell&#39;utente.

>[!CAUTION]
>
>I clientlibs di fogli di stile personalizzati devono essere caricati come parte dell&#39;intestazione affinché funzionino correttamente sia per l&#39;autore che per la pubblicazione.

## Abilita il componente Contenitore di layout per la pagina {#enable-the-layout-container-component-for-page}

Queste attività consentono agli autori di trascinare le istanze del componente **Contenitore di layout** sulla pagina.

### Abilitare il componente Contenitore di layout per la modifica della pagina {#enable-the-layout-container-component-for-page-editing}

Per consentire agli autori di aggiungere ulteriori griglie reattive alle pagine di contenuto, è necessario attivare il componente Contenitore di layout per la pagina. Potete eseguire questa operazione tramite:

* **Ambiente di authoring**

   Utilizzare la modalità [Progettazione](/help/sites-authoring/default-components-designmode.md) per attivare il componente **Contenitore livello** per una pagina.

* **Definizione componente**

   Per definire il componente, utilizzate `allowedComponent` o un&#39;inclusione statica.

### Configurare la griglia del contenitore di layout {#configure-the-grid-of-the-layout-container}

Potete configurare il numero di colonne disponibili per ogni istanza specifica di Contenitore di layout:

1. **Ambiente di authoring**

   Potete configurare il numero di colonne disponibili per ogni istanza specifica del Contenitore di layout.

   A questo scopo, utilizzate la modalità [Progettazione](/help/sites-authoring/default-components-designmode.md), quindi aprite la finestra di dialogo di progettazione per il contenitore richiesto. Qui è possibile specificare quante colonne saranno disponibili per il posizionamento e il ridimensionamento. Il valore predefinito è 12.

1. **XML**

   Le definizioni per la griglia reattiva sono specificate in:

   `etc/design/<*your-project-name*>/.content.xml`

   È possibile definire i seguenti parametri:

   * Numero di colonne disponibili:

      * `columns="{String}8"`
   * Componenti che possono essere aggiunti al componente corrente:

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`


