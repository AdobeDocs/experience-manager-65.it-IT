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
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 2%

---

# Configurazione del contenitore di layout e della modalità layout{#configuring-layout-container-and-layout-mode}

[Layout reattivo](/help/sites-authoring/responsive-layout.md) è un meccanismo per realizzare [design responsive](https://en.wikipedia.org/wiki/Responsive_web_design). Questo consente all’utente di creare pagine web con un layout e dimensioni che dipendono dai dispositivi utilizzati dagli utenti.

>[!NOTE]
>
>Questo può essere confrontato con il [Web mobile](/help/sites-developing/mobile-web.md) meccanismi, che utilizzano la progettazione web adattiva (principalmente per l’interfaccia utente classica).

AEM consente di realizzare il layout dinamico per le pagine utilizzando una combinazione di meccanismi:

* Componente [**Contenitore di layout**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)

  Questo componente fornisce un sistema paragrafo a griglia che consente di aggiungere e posizionare i componenti all’interno di una griglia reattiva. Può essere utilizzato come parsys predefinito per la pagina e/o reso disponibile agli autori nel browser componenti.

   * Il valore predefinito **Contenitore di layout** componente definito in:

     /libs/wcm/foundation/components/responsivegrid

   * Puoi definire i contenitori di layout:

      * Come componente che l’utente può aggiungere a una pagina.
      * Come parsys predefinito per la pagina.
      * Entrambi.

        Puoi avere il contenitore di layout come standard per la pagina, consentendo allo stesso tempo all’utente di aggiungere ulteriori contenitori di layout all’interno di questo; ad esempio, per ottenere il controllo delle colonne.

* **[Modalità Layout](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
Una volta che il contenitore di layout è posizionato sulla pagina, è possibile utilizzare **Layout** per posizionare il contenuto all’interno della griglia reattiva.

* [**Emulatore**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
Questo consente di creare e modificare siti web dinamici il cui layout si riorganizza in base alle dimensioni del dispositivo o della finestra, ridimensionando i componenti in modo interattivo. L’utente può quindi visualizzare come viene eseguito il rendering del contenuto utilizzando l’emulatore.

>[!CAUTION]
>
>Anche se il **Contenitore di layout** Il componente è disponibile nell’interfaccia classica; la sua piena funzionalità è disponibile solo nell’interfaccia touch.

Con questi meccanismi basati su una griglia dinamica è possibile:

* Utilizza i punti di interruzione (che indicano il raggruppamento del dispositivo) per definire un comportamento di contenuto diverso in base al layout del dispositivo.
* Nascondi i componenti in base al gruppo di dispositivi (definisci il punto di interruzione in cui un componente verrà nascosto).
* Utilizzate l&#39;aggancio orizzontale alla griglia (posizionate i componenti nella griglia, ridimensionate secondo necessità, definite quando comprimerli o rifluirli per essere affiancati o superiori/inferiori).
* Gestire il controllo delle colonne.

>[!NOTE]
>
>In un’installazione standard, il layout reattivo è stato configurato per [Sito di riferimento We.Retail](/help/sites-developing/we-retail.md). [Attivare il componente Contenitore di layout](#enable-the-layout-container-component-for-page) per altre pagine.

## Configurazione dell’emulatore reattivo {#configuring-the-responsive-emulator}

Questa attività ti consente di visualizzare **Emulatore** sul tuo sito.

### Registrare i componenti pagina per l’emulazione {#register-your-page-components-for-emulation}

Per abilitare l’emulatore a supportare le pagine, è necessario registrare i componenti della pagina. Consulta [Registrazione dei componenti della pagina per la simulazione](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### Specificare i gruppi di dispositivi {#specify-the-device-groups}

Per specificare i gruppi di dispositivi visualizzati nell&#39;elenco Dispositivi dell&#39;emulatore, vedere [Specifica dei gruppi di dispositivi](/help/sites-developing/responsive.md#specifying-the-device-groups).

### Collega il sito ai gruppi di dispositivi specificati {#link-your-site-to-the-specified-device-groups}

Per includere l’emulatore, collega il sito ai gruppi di dispositivi. Consulta [Aggiunta dell&#39;elenco dei dispositivi](/help/sites-developing/responsive.md#adding-the-devices-list) (sia per l’interfaccia utente classica che per quella ottimizzata per il tocco).

## Attiva modalità layout per il sito {#activate-layout-mode-for-your-site}

Queste procedure vengono utilizzate per **Layout** sul sito.

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
* Esiste un punto di interruzione predefinito (predefinito) che copre tutto ciò che si trova oltre l’ultimo *configurato* punto di interruzione.

Possono essere definiti utilizzando CRXDE Liti o XML.

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

#### Configurazione dei punti di interruzione tramite CRXDE Liti {#configuring-breakpoints-using-crxde-lite}

1. Utilizzando CRXDE Liti (o equivalente), accedi a:

   * Definizione del modello.
   * Il `jcr:content` della pagina.

1. Sotto `jcr:content` crea il nodo:

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

I punti di interruzione si trovano all&#39;interno del `<jcr:content>` sezione del `.context.html` nella cartella del modello (o del contenuto) appropriata.

Esempio di definizione:

```xml
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

Copia quanto segue `cq:infoProviders` struttura del nodo nel componente della pagina padre:

`/libs/foundation/components/page/cq:infoProviders/responsive`

## Abilita il ridimensionamento dei componenti per la pagina {#enable-component-resizing-for-the-page}

Queste procedure sono necessarie per poter ridimensionare i componenti in **Layout** modalità.

### Imposta contenitore layout come parsys principale {#set-layout-container-as-main-parsys}

Per impostare il parsys principale della pagina come contenitore di layout, definisci il parsys come:

`wcm/foundation/components/responsivegrid`

In:

* Componente pagina
* Modello pagina (per utilizzi futuri)

I due esempi seguenti illustrano la definizione:

* **HTL:**

  ```xml
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP:**

  ```
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### Includi CSS reattivo {#include-the-responsive-css}

#### CSS per i punti di interruzione che utilizzano MENO {#css-for-breakpoints-using-less}

AEM utilizza LESS per generare parti del CSS necessario, che devono essere incluse nei progetti.

Dovrai anche creare una [libreria client](https://experienceleague.adobe.com/docs/) per fornire chiamate di configurazione e funzione aggiuntive. Il seguente estratto LESS è un esempio del minimo da aggiungere al progetto:

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

Per ridimensionare e aggiornare correttamente il contenuto di un’immagine adattiva inclusa in una griglia reattiva, è necessario aggiungere una `afterEdit` imposta su `REFRESH_PAGE` listener in `EditConfig` file di ogni componente contenuto.

Ad esempio:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

Il meccanismo di immagine adattiva è reso disponibile tramite uno script che controlla la selezione dell’immagine corretta per le dimensioni correnti della finestra. Si attiva dopo che il DOM è pronto o quando si riceve un evento dedicato. Attualmente è necessario aggiornare la pagina per riflettere correttamente il risultato dell’azione dell’utente.

>[!CAUTION]
>
>Le clientlibs dei fogli di stile personalizzati devono essere caricate come parte dell’intestazione affinché funzionino correttamente durante l’authoring e la pubblicazione.

## Abilitare il componente Contenitore di layout per la pagina {#enable-the-layout-container-component-for-page}

Queste attività consentono agli autori di trascinare le istanze del **Contenitore di layout** sulla pagina.

### Abilitare il componente Contenitore di layout per la modifica delle pagine {#enable-the-layout-container-component-for-page-editing}

Per consentire agli autori di aggiungere ulteriori griglie reattive alle pagine di contenuto, devi abilitare il componente Contenitore di layout per la pagina. Puoi eseguire questa operazione utilizzando:

* **Ambiente di authoring**

  Utilizzare [Modalità progettazione](/help/sites-authoring/default-components-designmode.md) per attivare **Contenitore livello** per una pagina.

* **Definizione componente**

  Utilizzare `allowedComponent` o un inclusione statica durante la definizione del componente.

### Configurare la griglia del contenitore di layout {#configure-the-grid-of-the-layout-container}

Puoi configurare il numero di colonne disponibili per ogni istanza specifica del contenitore di layout:

1. **Ambiente di authoring**

   Puoi configurare il numero di colonne disponibili per ogni istanza specifica del contenitore di layout.

   A tale scopo, utilizza [Modalità progettazione](/help/sites-authoring/default-components-designmode.md), quindi apri la finestra di dialogo per progettazione del contenitore richiesto. Qui puoi specificare quante colonne saranno disponibili per il posizionamento e il dimensionamento. Il valore predefinito è 12.

1. **XML**

   Le definizioni per la griglia reattiva sono specificate in:

   `etc/design/<*your-project-name*>/.content.xml`

   È possibile definire i seguenti parametri:

   * Numero di colonne disponibili:

      * `columns="{String}8"`

   * Componenti che possono essere aggiunti al componente corrente:

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
