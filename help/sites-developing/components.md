---
title: Panoramica dei componenti
seo-title: Components
description: I componenti sono unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito web
seo-description: Components are modular units which realize specific functionality to present your content on your website
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 10%

---

# Panoramica dei componenti{#components-overview}

Questa pagina fornisce una panoramica dei componenti di Adobe Experience Manager (AEM) come quelli [utilizzato per l’authoring delle pagine](/help/sites-authoring/default-components-foundation.md).

## Cosa sono i Componenti? {#what-exactly-is-a-component}

* Unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito web.
* Riutilizzabile.
* Sviluppato come unità autonome all’interno di una cartella dell’archivio.
* Non sono presenti file di configurazione nascosti.
* Può contenere altri componenti.
* Può essere eseguito ovunque all&#39;interno di qualsiasi sistema AEM. Possono anche essere limitati all’esecuzione in componenti specifici.
* Avere un’interfaccia utente standard.
* Avere un comportamento di modifica configurabile.
* Utilizzare le finestre di dialogo create utilizzando elementi secondari basati sui componenti dell’interfaccia Granite
* Sono sviluppati utilizzando [HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html) (consigliato) o JSP.
* Può essere sviluppato per creare componenti personalizzati che estendono la funzionalità predefinita.

Poiché i componenti sono modulari, puoi:

* Sviluppa un nuovo componente nell’istanza locale.
* Distribuiscilo nell’ambiente di test.
* Distribuiscila nel tuo ambiente di authoring live, dove gli autori e/o gli amministratori possono aggiungere e configurare contenuti.
* Distribuiscila negli ambienti di pubblicazione live, dove viene utilizzata per il rendering dei contenuti per i visitatori del sito web. Alcuni componenti, ad esempio per Communities, accettano anche l’input degli utenti.

Ogni componente AEM:

* È un tipo di risorsa.
* È un insieme di script che realizzano completamente una funzione specifica.
* Ingresso *isolamento*, ovvero all’interno di AEM o di un portale.

## Componenti out-of-the-box in AEM {#out-of-the-box-components-within-aem}

AEM viene fornito con una varietà di [componenti predefiniti](/help/sites-authoring/default-components.md) che forniscono funzionalità complete, tra cui:

* Sistema paragrafo ( `parsys`)
* Pagina ( `responsivegrid` - solo interfaccia touch)
* Testo
* Immagine, con testo di accompagnamento
* Barra degli strumenti

I componenti forniti e il loro utilizzo all’interno della [siti web di esempio We.Retail](/help/sites-developing/we-retail.md) In vengono illustrate le modalità di implementazione e utilizzo dei componenti. I componenti sono forniti con tutto il codice sorgente e possono essere utilizzati così come sono o come punti di partenza per i componenti modificati o estesi.

### Componenti core e componenti di base {#core-components-and-foundation-components}

Sono disponibili due set di componenti AEM forniti da Adobe:

* [Componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html)
* [Componenti di base](/help/sites-authoring/default-components-foundation.md)

**Componenti core** sono stati introdotti con AEM 6.3 e offrono funzionalità di authoring flessibili e avanzate. La [Sito di riferimento We.Retail](/help/sites-developing/we-retail.md) illustra come utilizzare i componenti core e rappresentano le best practice correnti per lo sviluppo dei componenti.

**Componenti di base** sono disponibili con AEM per molte versioni e sono disponibili in un’installazione standard AEM. Sebbene ancora supportato, la maggior parte è stata dichiarata obsoleta, non viene più migliorata e si basa su tecnologie legacy.

>[!NOTE]
>
>[Componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) rappresentano le best practice correnti per la progettazione e lo sviluppo dei componenti e fungono da implementazioni di riferimento.
>
>[Strumenti di modernizzazione AEM](modernization-tools.md) può facilitare la migrazione ai componenti core.

### Visualizzazione dei componenti disponibili {#viewing-available-components}

Per una panoramica di tutti i componenti disponibili nell’istanza di AEM, utilizza la funzione [Console Componenti](/help/sites-authoring/default-components-console.md).

In alternativa, è possibile utilizzare CRXDE Lite per ottenere un elenco di tutti i componenti disponibili nell’archivio.

1. In **[!UICONTROL CRXDE Lite]**, seleziona **[!UICONTROL Strumenti]** dalla barra degli strumenti, quindi **[!UICONTROL Query]**, che apre la **[!UICONTROL Query]** scheda .

1. In **[!UICONTROL Query]** scheda , seleziona `XPath` come **[!UICONTROL Tipo]**.

1. Nel campo di inserimento **[!UICONTROL Query]** immettete la stringa seguente:

   `//element(*, cq:Component)`

1. Fai clic su **[!UICONTROL Esegui]** e i componenti sono elencati.

## Altro materiale di riferimento {#further-reading}

Le pagine seguenti forniscono informazioni più dettagliate sullo sviluppo di questi e altri componenti:

* [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md)
* [Sviluppo di componenti AEM](/help/sites-developing/developing-components.md)
* [Sviluppo di componenti AEM - Esempi di codice](/help/sites-developing/developing-components-samples.md)
* [Configurazione di più editor in-place](/help/sites-developing/multiple-inplace-editors.md)
* [Modalità Sviluppatore](/help/sites-developing/developer-mode.md)
* [Verifica dell’interfaccia utente](/help/sites-developing/hobbes.md)
* [Componenti per frammenti di contenuto](/help/sites-developing/components-content-fragments.md)
* [Ottenimento di informazioni di pagina in formato JSON](/help/sites-developing/pageinfo.md)
* [Componenti di internazionalizzazione](/help/sites-developing/i18n.md)
* [Componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [Utilizzo di Nascondi condizioni](/help/sites-developing/hide-conditions.md)
* Interfaccia classica

   * [Componenti AEM (interfaccia classica)](/help/sites-developing/developing-components-classic.md)
   * [Utilizzo ed estensione dei widget (interfaccia classica)](/help/sites-developing/widgets.md)
   * [Utilizzo di xtype (interfaccia classica)](/help/sites-developing/xtypes.md)
   * [Sviluppo di Forms (interfaccia classica)](/help/sites-developing/developing-forms.md)
