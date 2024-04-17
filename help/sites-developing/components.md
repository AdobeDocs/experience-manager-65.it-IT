---
title: Panoramica dei componenti
description: I componenti sono unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito web
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 44%

---

# Panoramica dei componenti{#components-overview}

Questa pagina fornisce una panoramica dei componenti di Adobe Experience Manager (AEM) come quelli [utilizzati per l’authoring delle pagine](/help/sites-authoring/default-components-foundation.md).

## Cosa sono i Componenti? {#what-exactly-is-a-component}

* Unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito web.
* Riutilizzabili.
* Sviluppati come unità autonome all’interno di una cartella dell’archivio.
* Non sono presenti file di configurazione nascosti.
* Possono contenere altri componenti.
* Può essere eseguito ovunque all&#39;interno di qualsiasi sistema AEM. Possono anche essere limitate per l’esecuzione con componenti specifici.
* Hanno un’interfaccia utente standard.
* Hanno un comportamento di modifica configurabile.
* Utilizzare finestre di dialogo create utilizzando sottoelementi basati su componenti dell’interfaccia utente Granite
* Sono sviluppati utilizzando [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it) (consigliato) o JSP.
* Possono essere sviluppati per creare componenti personalizzati che estendono la funzionalità predefinita.

Poiché i componenti sono modulari, puoi:

* Sviluppare un nuovo componente nell’istanza locale.
* Distribuirlo nell’ambiente di test.
* Distribuirlo nel tuo ambiente di authoring live, dove gli autori e/o gli amministratori possono aggiungere e configurare contenuti.
* Distribuiscilo negli ambienti di pubblicazione live, dove viene utilizzato per eseguire il rendering dei contenuti per i visitatori del tuo sito web. Alcuni componenti, ad esempio per Communities, accettano l’input anche dagli utenti.

Ogni componente AEM:

* È un tipo di risorsa.
* È un insieme di script che realizzano completamente una funzione specifica.
* Può funzionare in *isolamento*, ovvero all&#39;interno dell&#39;AEM o di un portale.

## Componenti standard all’interno dell’AEM {#out-of-the-box-components-within-aem}

L&#39;AEM viene fornito con una varietà di [componenti pronti all’uso](/help/sites-authoring/default-components.md) che offrono funzionalità complete, tra cui:

* Sistema paragrafi ( `parsys`)
* Pagina ( `responsivegrid` - solo interfaccia touch)
* Testo
* Immagine, con testo associato
* Barra degli strumenti

I componenti forniti e il loro utilizzo all’interno del [siti Web We.Retail di esempio](/help/sites-developing/we-retail.md) fornite illustrano come implementare e utilizzare i componenti. I componenti sono forniti con tutto il codice sorgente e possono essere utilizzati così come sono o come punti di partenza per i componenti modificati o estesi.

### Componenti core e componenti di base {#core-components-and-foundation-components}

Sono disponibili due set di componenti AEM forniti dall’Adobe:

* [Componenti di base](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)
* [Componenti di base](/help/sites-authoring/default-components-foundation.md)

**Componenti core** sono state introdotte con AEM 6.3 e offrono funzionalità flessibili e avanzate per l’authoring. Il [Sito di riferimento We.Retail](/help/sites-developing/we-retail.md) illustra come utilizzare i Componenti core e le best practice per lo sviluppo dei componenti.

**Componenti di base** sono disponibili con AEM per molte versioni e sono preconfigurati in un’installazione standard per AEM. Anche se ancora supportate, la maggior parte sono state dichiarate obsolete, non sono più migliorate e si basano su tecnologie legacy.

>[!NOTE]
>
>[Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) rappresenta le best practice correnti per la progettazione e lo sviluppo dei componenti e funge da implementazioni di riferimento.
>
>[Strumenti di modernizzazione AEM](modernization-tools.md) può agevolare la migrazione ai Componenti core.

### Visualizzazione dei componenti disponibili {#viewing-available-components}

Per una panoramica di tutti i componenti disponibili nell’istanza AEM, utilizza [Console Componenti](/help/sites-authoring/default-components-console.md).

In alternativa, è possibile utilizzare CRXDE Lite per ottenere un elenco di tutti i componenti disponibili nell’archivio.

1. In **[!UICONTROL CRXDE Lite]**, seleziona **[!UICONTROL Strumenti]** dalla barra degli strumenti, quindi **[!UICONTROL Query]**, che apre la scheda **[!UICONTROL Query]**.

1. Nella scheda **[!UICONTROL Query]**, seleziona `XPath` come **[!UICONTROL Tipo]**.

1. Nel campo di inserimento **[!UICONTROL Query]**, immetti la stringa seguente:

   `//element(*, cq:Component)`

1. Fai clic su **[!UICONTROL Esegui]** e i componenti verranno elencati.

## Risorse aggiuntive {#further-reading}

Le pagine seguenti forniscono informazioni più dettagliate sullo sviluppo di questi e di altri componenti:

* [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md)
* [Sviluppo di componenti AEM](/help/sites-developing/developing-components.md)
* [Sviluppo di componenti AEM - Esempi di codice](/help/sites-developing/developing-components-samples.md)
* [Configurazione di più editor locali](/help/sites-developing/multiple-inplace-editors.md)
* [Modalità Sviluppatore](/help/sites-developing/developer-mode.md)
* [Verifica dell’interfaccia utente](/help/sites-developing/hobbes.md)
* [Componenti per frammenti di contenuto](/help/sites-developing/components-content-fragments.md)
* [Ottenimento delle informazioni di pagina in formato JSON](/help/sites-developing/pageinfo.md)
* [Internazionalizzazione dei componenti](/help/sites-developing/i18n.md)
* [Componenti di base](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)
* [Utilizzo di Nascondi condizioni](/help/sites-developing/hide-conditions.md)
* Interfaccia classica

   * [Componenti AEM (interfaccia classica)](/help/sites-developing/developing-components-classic.md)
   * [Utilizzo ed estensione dei widget (interfaccia classica)](/help/sites-developing/widgets.md)
   * [Utilizzo di xtypes (interfaccia classica)](/help/sites-developing/xtypes.md)
   * [Sviluppo di Forms (interfaccia classica)](/help/sites-developing/developing-forms.md)
