---
title: Funzionalità di layout dei moduli adattivi
seo-title: Layout capabilities of adaptive forms
description: Il layout e l’aspetto dei moduli adattivi su vari dispositivi sono disciplinati dalle impostazioni di layout. Comprendere i vari layout e come applicarli.
seo-description: Layout and appearances of adaptive forms on various devices are governed by the layout settings. Understand the various layouts and how to apply them.
uuid: 79022ac2-1aa3-47c5-b094-cbe83334ea62
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
feature: Adaptive Forms
exl-id: 3db623a4-f1ad-4b7f-97e8-0be138aa8b26
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---

# Funzionalità di layout dei moduli adattivi{#layout-capabilities-of-adaptive-forms}

Adobe Experience Manager (AEM) consente di creare moduli adattivi facili da usare che offrono esperienze dinamiche agli utenti finali. Il layout del modulo controlla il modo in cui gli elementi o i componenti vengono visualizzati in un modulo adattivo.

## Conoscenze preliminari {#prerequisite-knowledge}

Prima di scoprire le diverse funzionalità di layout dei moduli adattivi, leggi i seguenti articoli per ulteriori informazioni sui moduli adattivi.

[Introduzione ad AEM Forms](../../forms/using/introduction-aem-forms.md)

[Introduzione all’authoring dei moduli](../../forms/using/introduction-forms-authoring.md)

## Tipi di layout {#types-of-layouts}

Un modulo adattivo offre i seguenti tipi di layout:

**Layout pannello** Controlla il modo in cui gli elementi o i componenti all&#39;interno di un pannello vengono visualizzati su un dispositivo.

**Layout dispositivo mobile** Controlla la navigazione di un modulo su un dispositivo mobile. Se la larghezza del dispositivo è di 768 pixel o più, il layout viene considerato un layout mobile e ottimizzato per un dispositivo mobile.

**Layout barra degli strumenti** Controlla il posizionamento dei pulsanti di azione nella barra degli strumenti o nel pannello di un modulo.

Tutti questi layout di pannello sono definiti nella posizione seguente:

`/libs/fd/af/layouts`.

>[!NOTE]
>
>Per modificare il layout di un modulo adattivo, utilizza la Modalità di authoring in AEM.

![Posizione dei layout nell’archivio CRX](assets/layouts_location_in_crx.png)

## Layout pannello {#panel-layout}

Un autore di moduli può associare un layout a ciascun pannello di un modulo adattivo, incluso il pannello principale.

I layout del pannello sono disponibili all&#39;indirizzo `/libs/fd/af/layouts/panel` posizione.

![Elenco dei layout dei pannelli per il pannello principale di un modulo adattivo](assets/layouts.png)

Elenco dei layout dei pannelli nei moduli adattivi

### Reattivo - tutto su una pagina senza navigazione {#responsive-everything-on-one-page-without-navigation-br}

Utilizza questo layout di pannello per creare un layout reattivo che si adatta alle dimensioni dello schermo del dispositivo senza alcuna necessità di navigazione specializzata.

Utilizzando questo layout, è possibile inserire più **[!UICONTROL Modulo adattivo per pannello]** componenti uno dopo l’altro all’interno del pannello.

![Un modulo che utilizza il layout dinamico come visualizzato su un piccolo schermo](assets/responsive_layout_seen_on_small_screen.png)

Un modulo che utilizza il layout dinamico come visualizzato su un piccolo schermo

![Un modulo che utilizza il layout dinamico come visualizzato su un grande schermo](assets/responsive_layout_seen_on_large_screen.png)

Un modulo che utilizza il layout dinamico come visualizzato su un grande schermo

### Procedura guidata: un modulo con più passaggi che mostra un passaggio alla volta {#wizard-a-multi-step-form-showing-one-step-at-a-time}

Utilizza questo layout di pannello per fornire una navigazione guidata all’interno di un modulo. Utilizzare ad esempio questo layout per acquisire informazioni obbligatorie in un modulo guidando gli utenti passo dopo passo.

Utilizza il `Panel adaptive form` per una navigazione dettagliata all’interno di un pannello. Quando utilizzi questo layout, un utente passa al passaggio successivo solo dopo aver completato il passaggio corrente

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![Espressione di completamento passaggio nel layout della procedura guidata per un modulo con più passaggi](assets/layout-sidebar.png)

Espressione di completamento passaggio nel layout della procedura guidata per un modulo con più passaggi

![Un modulo che utilizza il layout della procedura guidata](assets/wizard-layout.png)

Maschera che utilizza la procedura guidata

### Layout per il pannello a soffietto {#layout-for-accordion-design}

Utilizzando questo layout, è possibile inserire `Panel adaptive form` componente in un pannello con navigazione in stile Pannello a soffietto. Utilizzando questo layout, puoi anche creare pannelli ripetibili. I pannelli ripetibili consentono di aggiungere o rimuovere in modo dinamico i pannelli in base alle esigenze. Puoi definire il numero minimo e massimo di ripetizioni di un pannello. Inoltre, il titolo del pannello può essere determinato dinamicamente, in base alle informazioni fornite negli elementi del pannello.

L’espressione di riepilogo può essere utilizzata per mostrare i valori forniti dall’utente finale nel titolo del pannello ridotto a icona.

![Pannelli ripetibili con layout a soffietto nei moduli adattivi](assets/repeatable_panels_using_accordion_layout.png)

Pannelli ripetibili creati con il layout Pannello a soffietto

### Layout a schede: le schede vengono visualizzate a sinistra {#tabbed-layout-tabs-appear-on-the-left}

Utilizzando questo layout, è possibile inserire `Panel adaptive form` componente in un pannello con navigazione tramite schede. Le schede vengono posizionate a sinistra del contenuto del pannello.

![Nel layout con schede, le schede vengono visualizzate a sinistra](assets/tabbed_layout_left.png)

Schede visualizzate a sinistra di un pannello

### Layout a schede: le schede vengono visualizzate nella parte superiore {#tabbed-layout-tabs-appear-on-the-top}

Utilizzando questo layout, è possibile inserire `Panel adaptive form` Componente in un pannello con navigazione tramite schede. Le schede vengono posizionate sopra il contenuto del pannello.

![Layout a schede nei moduli adattivi con schede nella parte superiore](assets/tabbed_layout_top.png)

Schede visualizzate nella parte superiore di un pannello

## Layout dispositivi mobili {#mobile-layouts}

I layout mobili consentono una navigazione semplice sui dispositivi mobili con schermi relativamente più piccoli. I layout mobili utilizzano gli stili a schede o della procedura guidata per la navigazione dei moduli. L’applicazione di un layout mobile fornisce un unico layout per l’intero modulo.

Questo layout controlla la navigazione tramite una barra di navigazione e un menu di navigazione. La barra di navigazione mostra **&lt;** e **>** icona per indicare **avanti** e **precedente** passaggi di navigazione nel modulo.

I layout per dispositivi mobili sono disponibili all’indirizzo `/libs/fd/af/layouts/mobile/` posizione. Per impostazione predefinita, i seguenti layout per dispositivi mobili sono disponibili nei moduli adattivi.

![Elenco dei layout mobili nei moduli adattivi](assets/mobile-navigation.png)

Elenco dei layout mobili nei moduli adattivi

Quando si utilizza un layout mobile, per accedere a vari pannelli del modulo tocca il menu del modulo ![aem6forms_form_menu](assets/aem6forms_form_menu.png) icona.

### Layout con titoli dei pannelli nell’intestazione del modulo {#layout-with-panel-titles-in-the-form-header}

Questo layout, come suggerisce il nome, mostra i titoli dei pannelli insieme al menu di navigazione e alla barra di navigazione. Questo layout fornisce anche le icone Successivo e Precedente per la navigazione.

![Layout mobili con titoli dei pannelli nelle intestazioni dei moduli](assets/mobile_layout_with.png)

Layout mobili con titoli dei pannelli nelle intestazioni dei moduli

### Layout senza titoli dei pannelli nell’intestazione del modulo {#layout-without-panel-titles-in-the-form-header}

Come suggerisce il nome, questo layout mostra solo il menu di navigazione e la barra di navigazione senza i titoli dei pannelli. Questo layout fornisce anche le icone Successivo e Precedente per la navigazione.

![Layout mobili senza titoli dei pannelli nelle intestazioni dei moduli](assets/mobile_layout_without.png)

Layout mobili senza titoli dei pannelli nelle intestazioni dei moduli

## Layout della barra degli strumenti {#toolbar-layouts}

Un layout a barre degli strumenti controlla il posizionamento e la visualizzazione di eventuali pulsanti di azione aggiunti ai moduli adattivi. Il layout può essere aggiunto a livello di modulo o di pannello.

![Elenco dei layout della barra degli strumenti nei moduli adattivi per controllare il layout dei pulsanti](assets/toolbar-layouts.png)

Elenco dei layout delle barre degli strumenti nei moduli adattivi

I layout della barra degli strumenti sono disponibili all&#39;indirizzo `/libs/fd/af/layouts/toolbar` posizione. per impostazione predefinita, i moduli adattivi forniscono i seguenti layout di barra degli strumenti.

### Layout predefinito per la barra degli strumenti {#default-layout-for-toolbar}

Questo layout viene selezionato come layout predefinito quando aggiungi pulsanti di azione in un modulo adattivo. Selezionando questo layout viene visualizzato lo stesso layout sia per i dispositivi desktop che per quelli mobili.

Inoltre, è possibile aggiungere più barre degli strumenti contenenti pulsanti di azione configurati con questo layout. Un pulsante di azione è associato a un controllo modulo. È possibile configurare le barre degli strumenti in modo che siano prima o dopo un pannello.

![Visualizzazione predefinita per la barra degli strumenti](assets/toolbar_layout_default.png)

Visualizzazione predefinita per la barra degli strumenti

### Layout fisso mobile per barra degli strumenti {#mobile-fixed-layout-for-toolbar}

Selezionare questo layout per fornire layout alternativi per desktop e dispositivi mobili.

Per il layout del desktop, è possibile aggiungere pulsanti di azione utilizzando alcune etichette specifiche. Con questo layout è possibile configurare una sola barra degli strumenti. Se con questo layout sono configurate più barre degli strumenti, esiste una sovrapposizione per i dispositivi mobili e una sola barra degli strumenti è visibile. È possibile ad esempio disporre di una barra degli strumenti nella parte inferiore o superiore del modulo oppure, dopo o prima dei pannelli del modulo.

Per il layout mobile, puoi aggiungere pulsanti di azione utilizzando le icone.

![Layout fisso mobile per barra degli strumenti](assets/toolbar_layout_mobile_fixed.png)

Layout fisso mobile per barra degli strumenti
