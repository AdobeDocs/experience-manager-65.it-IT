---
title: Funzionalità di layout dei moduli adattivi
seo-title: Funzionalità di layout dei moduli adattivi
description: Il layout e l'aspetto dei moduli adattivi su vari dispositivi sono regolati dalle impostazioni di layout. Comprendere i vari layout e come applicarli.
seo-description: Il layout e l'aspetto dei moduli adattivi su vari dispositivi sono regolati dalle impostazioni di layout. Comprendere i vari layout e come applicarli.
uuid: 79022ac2-1aa3-47c5-b094-cbe83334ea62
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---


# Funzionalità di layout dei moduli adattivi{#layout-capabilities-of-adaptive-forms}

 Adobe Experience Manager (AEM) consente di creare moduli adattivi di facile utilizzo che offrono esperienze dinamiche agli utenti finali. Il layout del modulo controlla il modo in cui gli elementi o i componenti vengono visualizzati in un modulo adattivo.

## Conoscenza dei prerequisiti {#prerequisite-knowledge}

Prima di apprendere le diverse funzionalità di layout dei moduli adattivi, consultare i seguenti articoli per ulteriori informazioni sui moduli adattivi.

[Introduzione ai AEM Forms](../../forms/using/introduction-aem-forms.md)

[Introduzione alla creazione di moduli](../../forms/using/introduction-forms-authoring.md)

## Tipi di layout {#types-of-layouts}

Un modulo adattivo fornisce i seguenti tipi di layout:

**Layout** pannello Controlla il modo in cui gli elementi o i componenti all’interno di un pannello vengono visualizzati su un dispositivo.

**Layout** mobile Controlla la navigazione di un modulo su un dispositivo mobile. Se la larghezza del dispositivo è pari o superiore a 768 pixel, il layout viene considerato mobile e ottimizzato per un dispositivo mobile.

**Layout** barra degli strumenti Controlla la posizione dei pulsanti Azione nella barra degli strumenti o nella barra degli strumenti di un modulo.

Tutti i layout di questi pannelli sono definiti nella posizione seguente:

`/libs/fd/af/layouts`.

>[!NOTE]
>
>Per modificare il layout di un modulo adattivo, utilizzate la modalità Authoring in AEM.

![Posizione dei layout nel repository CRX](assets/layouts_location_in_crx.png)

## Layout pannello {#panel-layout}

Un autore di un modulo può associare un layout a ciascun pannello di un modulo adattivo, incluso il pannello principale.

I layout del pannello sono disponibili nella `/libs/fd/af/layouts/panel` posizione desiderata.

![Elenco di layout di pannelli per il pannello principale di un modulo adattivo](assets/layouts.png)

Elenco dei layout dei pannelli nei moduli adattivi

### Responsive - everything on one page without navigation {#responsive-everything-on-one-page-without-navigation-br}

Utilizzate questo layout del pannello per creare un layout reattivo che si adatti alle dimensioni dello schermo del dispositivo senza necessità di navigazione specializzata.

Utilizzando questo layout, è possibile posizionare più componenti modulo **[!UICONTROL adattivo per]** pannello uno dopo l’altro all’interno del pannello.

![Un modulo con layout reattivo come visualizzato su uno schermo di piccole dimensioni](assets/responsive_layout_seen_on_small_screen.png)

Un modulo con layout reattivo come visualizzato su uno schermo di piccole dimensioni

![Un modulo con layout reattivo come visualizzato su uno schermo grande](assets/responsive_layout_seen_on_large_screen.png)

Un modulo con layout reattivo come visualizzato su uno schermo grande

### Procedura guidata: un modulo con più fasi che mostra un passaggio alla volta {#wizard-a-multi-step-form-showing-one-step-at-a-time}

Utilizzare questo layout del pannello per fornire la navigazione guidata all&#39;interno di un modulo. Ad esempio, utilizzare questo layout per acquisire informazioni obbligatorie in un modulo e guidare gli utenti passo dopo passo.

Usate il `Panel adaptive form` componente per effettuare una navigazione dettagliata all’interno di un pannello. Quando utilizzate questo layout, un utente passa al passaggio successivo solo dopo che il passaggio corrente è stato completato

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![Espressione completamento passo nel layout Procedura guidata per un modulo a più fasi](assets/layout-sidebar.png)

Espressione completamento passo nel layout Procedura guidata per un modulo a più fasi

![Un modulo con layout guidato](assets/wizard-layout.png)

Un modulo che utilizza la procedura guidata

### Layout per la progettazione a soffietto {#layout-for-accordion-design}

Utilizzando questo layout, potete posizionare il `Panel adaptive form` componente in un pannello con navigazione in stile Accordion. Utilizzando questo layout, potete anche creare pannelli ripetibili. I pannelli ripetibili consentono di aggiungere o rimuovere i pannelli in modo dinamico in base alle esigenze. Potete definire il numero minimo e massimo di ripetizioni di un pannello. Inoltre, il titolo del pannello può essere determinato in modo dinamico, in base alle informazioni fornite negli elementi del pannello.

L&#39;espressione Summary può essere utilizzata per mostrare i valori forniti dall&#39;utente finale nel titolo del pannello ridotto a icona.

![Pannelli ripetibili con layout a soffietto nei moduli adattivi](assets/repeatable_panels_using_accordion_layout.png)

Pannelli ripetibili creati con il layout a soffietto

### Layout a schede - le schede vengono visualizzate a sinistra {#tabbed-layout-tabs-appear-on-the-left}

Utilizzando questo layout, potete posizionare il `Panel adaptive form` componente in un pannello con la navigazione tramite scheda. Le schede vengono posizionate a sinistra del contenuto del pannello.

![Nel layout a schede, le schede vengono visualizzate a sinistra](assets/tabbed_layout_left.png)

Schede visualizzate a sinistra di un pannello

### Layout a schede - le schede vengono visualizzate nella parte superiore {#tabbed-layout-tabs-appear-on-the-top}

Utilizzando questo layout, è possibile posizionare il `Panel adaptive form` componente in un pannello con la navigazione tramite scheda. Le schede vengono posizionate sopra al contenuto del pannello.

![Layout a schede nei moduli adattivi con schede nella parte superiore](assets/tabbed_layout_top.png)

Schede visualizzate nella parte superiore di un pannello

## Layout per dispositivi mobili {#mobile-layouts}

I layout per dispositivi mobili consentono una navigazione semplice sui dispositivi mobili con schermate relativamente più piccole. I layout per dispositivi mobili utilizzano stili a schede o procedure guidate per la navigazione del modulo. L&#39;applicazione di un layout mobile fornisce un singolo layout per l&#39;intero modulo.

Questo layout controlla la navigazione mediante una barra di navigazione e un menu di navigazione. La barra di navigazione mostra l&#39;icona **&lt;** e **>** per indicare i passaggi di navigazione **successivi** e **precedenti** nel modulo.

I layout per dispositivi mobili sono disponibili nella `/libs/fd/af/layouts/mobile/` posizione. Per impostazione predefinita, nei moduli adattivi sono disponibili i seguenti layout per dispositivi mobili.

![Elenco dei layout per dispositivi mobili nei moduli adattivi](assets/mobile-navigation.png)

Elenco dei layout per dispositivi mobili nei moduli adattivi

Quando si utilizza un layout mobile, il menu del modulo, per accedere ai vari pannelli del modulo, è disponibile toccando l&#39;icona ![aem6forms_form_menu](assets/aem6forms_form_menu.png) .

### Layout con titoli del pannello nell’intestazione del modulo {#layout-with-panel-titles-in-the-form-header}

Questo layout, come suggerisce il nome, mostra i titoli dei pannelli insieme al menu di navigazione e alla barra di navigazione. Questo layout include anche le icone Successivo e Precedente per la navigazione.

![Layout per dispositivi mobili con titoli dei pannelli nelle intestazioni del modulo](assets/mobile_layout_with.png)

Layout per dispositivi mobili con titoli dei pannelli nelle intestazioni del modulo

### Layout senza titoli del pannello nell&#39;intestazione del modulo {#layout-without-panel-titles-in-the-form-header}

Questo layout, come suggerisce il nome, mostra solo il menu di navigazione e la barra di navigazione senza titoli del pannello. Questo layout include anche le icone Successivo e Precedente per la navigazione.

![Layout per dispositivi mobili senza titoli del pannello nelle intestazioni del modulo](assets/mobile_layout_without.png)

Layout per dispositivi mobili senza titoli del pannello nelle intestazioni del modulo

## Layout della barra degli strumenti {#toolbar-layouts}

Un Layout barra degli strumenti controlla la posizione e la visualizzazione di eventuali pulsanti di azione aggiunti ai moduli adattivi. Il layout può essere aggiunto a livello di modulo o di pannello.

![Elenco dei layout della barra degli strumenti nei moduli adattivi per controllare il layout dei pulsanti](assets/toolbar-layouts.png)

Elenco dei layout della barra degli strumenti nei moduli adattivi

I layout della barra degli strumenti sono disponibili in `/libs/fd/af/layouts/toolbar` loco. per impostazione predefinita, i moduli adattivi forniscono i seguenti layout della barra degli strumenti.

### Layout predefinito per la barra degli strumenti {#default-layout-for-toolbar}

Questo layout viene selezionato come layout predefinito quando si aggiungono pulsanti di azione in un modulo adattivo. Selezionando questo layout viene visualizzato lo stesso layout sia per desktop che per dispositivi mobili.

È inoltre possibile aggiungere più barre degli strumenti contenenti pulsanti di azione configurati con questo layout. Un pulsante di azione è associato a un controllo modulo. È possibile configurare le barre degli strumenti prima o dopo un pannello.

![Vista predefinita per la barra degli strumenti](assets/toolbar_layout_default.png)

Vista predefinita per la barra degli strumenti

### Layout fisso per dispositivi mobili per la barra degli strumenti {#mobile-fixed-layout-for-toolbar}

Selezionate questo layout per fornire layout alternativi per desktop e dispositivi mobili.

Per il layout desktop, è possibile aggiungere pulsanti Azione utilizzando alcune etichette specifiche. Con questo layout è possibile configurare una sola barra degli strumenti. Se con questo layout sono configurate più barre degli strumenti, esiste una sovrapposizione per i dispositivi mobili e una sola barra degli strumenti è visibile. Ad esempio, è possibile avere una barra degli strumenti nella parte inferiore o superiore del modulo, dopo o prima dei pannelli nel modulo.

Per il layout mobile, potete aggiungere pulsanti di azione utilizzando delle icone.

![Layout fisso per dispositivi mobili per la barra degli strumenti](assets/toolbar_layout_mobile_fixed.png)

Layout fisso per dispositivi mobili per la barra degli strumenti

