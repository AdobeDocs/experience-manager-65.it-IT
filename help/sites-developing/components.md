---
title: Componenti Panoramica
seo-title: Componenti
description: I componenti sono unità modulari che offrono funzionalità specifiche per presentare i contenuti sul sito Web
seo-description: I componenti sono unità modulari che offrono funzionalità specifiche per presentare i contenuti sul sito Web
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 9%

---


# Panoramica dei componenti{#components-overview}

Questa pagina fornisce una panoramica dei componenti Adobe Experience Manager (AEM) come quelli [utilizzati per l&#39;authoring delle pagine](/help/sites-authoring/default-components-foundation.md).

## Cosa sono i componenti? {#what-exactly-is-a-component}

* Unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito Web.
* Riutilizzabile.
* Sviluppato come unità indipendenti all’interno di una cartella del repository.
* Non hanno file di configurazione nascosti.
* Può contenere altri componenti.
* Può essere eseguito ovunque all&#39;interno di qualsiasi sistema AEM. Possono anche essere limitati per essere eseguiti con componenti specifici.
* Avere un&#39;interfaccia utente standard.
* Avere un comportamento di modifica configurabile.
* Utilizzare le finestre di dialogo create utilizzando sottoelementi basati sui componenti dell&#39;interfaccia utente Granite
* Sono sviluppati utilizzando [HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html) (consigliato) o JSP.
* Può essere sviluppato per creare componenti personalizzati che estendono le funzionalità predefinite.

Poiché i componenti sono modulari, potete:

* Sviluppare un nuovo componente nell’istanza locale.
* Distribuitelo nell&#39;ambiente di test.
* Potrai distribuirli nel tuo ambiente di authoring dal vivo, in cui gli autori e/o gli amministratori possono aggiungere e configurare contenuti.
* Distribuitelo negli ambienti di pubblicazione dal vivo, dove vengono usati per eseguire il rendering dei contenuti per i visitatori del sito Web. Alcuni componenti, ad esempio per Community, accettano anche l’input degli utenti.

Ciascun componente AEM:

* È un tipo di risorsa.
* È un insieme di script che realizza completamente una funzione specifica.
* Può funzionare in *isolamento*, ovvero all&#39;interno di AEM o di un portale.

## Componenti out-of-the-box in AEM {#out-of-the-box-components-within-aem}

AEM viene fornito con una serie di [componenti out-of-the-box](/help/sites-authoring/default-components.md) che forniscono funzionalità complete, tra cui:

* Sistema paragrafo ( `parsys`)
* Pagina ( `responsivegrid` - solo interfaccia touch)
* Testo
* Immagine, con testo di accompagnamento
* Barra degli strumenti

I componenti forniti e il loro utilizzo all&#39;interno dei [siti Web di esempio We.Retail](/help/sites-developing/we-retail.md) forniti illustrano come implementare e usare i componenti. I componenti sono forniti con tutto il codice sorgente e possono essere utilizzati come punti di partenza per componenti modificati o estesi.

### Componenti di base e componenti di base {#core-components-and-foundation-components}

Sono disponibili due set di  componenti AEM forniti dal Adobe:

* [Componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html)
* [Componenti di base](/help/sites-authoring/default-components-foundation.md)

**I** componenti core sono stati introdotti con AEM 6.3 e offrono funzionalità di authoring flessibili e avanzate. Il sito di riferimento [We.Retail](/help/sites-developing/we-retail.md) illustra come i componenti core possono essere utilizzati e rappresenta le procedure ottimali correnti per lo sviluppo dei componenti.

**Foundation** Componentshsono disponibili con AEM per molte versioni e sono disponibili out-of-the-box in un&#39;installazione AEM standard. Anche se ancora supportati, la maggior parte sono stati dichiarati obsoleti, non vengono più migliorati e si basano su tecnologie legacy.

>[!NOTE]
>
>[I ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) componenti core rappresentano le best practice correnti per la progettazione e lo sviluppo di componenti e fungono da implementazioni di riferimento.
>
>[AEM Modernization ](modernization-tools.md) Toolscan facilita la migrazione ai componenti core.

### Visualizzazione dei componenti disponibili {#viewing-available-components}

Per una panoramica di tutti i componenti disponibili nell&#39;istanza di AEM, utilizzate la [console Componenti](/help/sites-authoring/default-components-console.md).

In alternativa, potete anche utilizzare CRXDE Lite per ottenere un elenco di tutti i componenti disponibili nella directory archivio.

1. In **[!UICONTROL CRXDE Lite]**, selezionare **[!UICONTROL Strumenti]** dalla barra degli strumenti, quindi **[!UICONTROL Query]**, che apre la scheda **[!UICONTROL Query]**.

1. Nella scheda **[!UICONTROL Query]**, selezionare `XPath` come **[!UICONTROL Tipo]**.

1. Nel campo di inserimento **[!UICONTROL Query]** immettete la stringa seguente:

   `//element(*, cq:Component)`

1. Fare clic su **[!UICONTROL Esegui]** per elencare i componenti.

## Altro materiale di riferimento {#further-reading}

Le pagine seguenti forniscono informazioni più dettagliate sullo sviluppo di questi e altri componenti:

* [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md)
* [Sviluppo di componenti AEM](/help/sites-developing/developing-components.md)
* [Sviluppo di componenti AEM - Esempi di codice](/help/sites-developing/developing-components-samples.md)
* [Configurazione di più editor interni](/help/sites-developing/multiple-inplace-editors.md)
* [Modalità Sviluppatore](/help/sites-developing/developer-mode.md)
* [Verifica dell’interfaccia](/help/sites-developing/hobbes.md)
* [Componenti per frammenti di contenuto](/help/sites-developing/components-content-fragments.md)
* [Ottenimento di informazioni sulla pagina in formato JSON](/help/sites-developing/pageinfo.md)
* [Internazionalizzazione dei componenti](/help/sites-developing/i18n.md)
* [Componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [Utilizzo di Nascondi condizioni](/help/sites-developing/hide-conditions.md)
* Interfaccia classica

   * [Componenti AEM (interfaccia classica)](/help/sites-developing/developing-components-classic.md)
   * [Utilizzo ed estensione dei widget (interfaccia classica)](/help/sites-developing/widgets.md)
   * [Utilizzo di xtype (interfaccia classica)](/help/sites-developing/xtypes.md)
   * [Sviluppo di Forms (interfaccia classica)](/help/sites-developing/developing-forms.md)

