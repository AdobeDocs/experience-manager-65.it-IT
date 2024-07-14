---
title: Panoramica dei modelli
description: Scopri come utilizzare la gestione dei modelli, che prevede la creazione e la gestione di modelli da associare a eventuali oggetti dati.
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 50785534-5784-4354-b123-5e640b7c0242
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 0%

---

# Panoramica dei modelli{#models-overview}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

La gestione dei modelli comporta la creazione e la gestione di modelli per l’associazione a eventuali oggetti dati. Ogni modello include tutte le proprietà e le definizioni dei campi necessarie per facilitare la creazione e il rendering degli oggetti.

Gestione modelli prevede la creazione di **modelli**, **entità** e **spazi**. Il diagramma seguente illustra la relazione tra il contenuto dell’AEM e i modelli.

![chlimage_1-81](assets/chlimage_1-81.png)

## Il modello di contenuto {#the-content-model}

Un modello descrive il tipo di contenuto e indica quali informazioni sono disponibili per l&#39;applicazione nativa. È una descrizione di ciò che costituisce un contenuto. Un modello di contenuto è costituito dalle regole per la creazione di un contenuto. Il modello di contenuto include i dati disponibili, le risorse utilizzabili, la relazione tra risorse e dati, la relazione con altri modelli di contenuto e i metadati disponibili.

I modelli fungono anche da modo per trasformare i contenuti AEM esistenti in oggetti che possono essere facilmente utilizzati dalle app native per dispositivi mobili.

Content Services fornisce alcuni modelli predefiniti per oggetti comuni come risorse, raccolte di risorse, pagine HTML, configurazioni di app e pagine indipendenti dal canale. Sono configurabili in modo da soddisfare le esigenze specifiche dei clienti senza richiedere attività di sviluppo per l’AEM.

Gli utenti possono creare i propri modelli. In questo modo è possibile creare nuovi tipi di contenuto non ancora gestiti dall’AEM. La creazione del modello viene eseguita tramite un&#39;interfaccia utente che utilizza i tipi primitivi esistenti.

Il diagramma seguente illustra il modello di contenuto per le app AEM Mobile e il modo in cui entità, cartelle e spazi vengono assegnati a un’app.

![chlimage_1-82](assets/chlimage_1-82.png)

### Modelli {#the-models}

I modelli vengono utilizzati per determinare la modalità di creazione delle entità. Definiscono cosa è disponibile in un’entità e come quei dati vengono generati dal contenuto dell’AEM. Prima di iniziare a lavorare con spazi, cartelle ed entità, è necessario avere familiarità con la creazione e la gestione dei modelli.

>[!NOTE]
>
>Esiste un modello all’esterno di un’app, poiché può essere utilizzato da più app.
>

Per creare e gestire modelli nel dashboard e nel repository, vedere **[Modelli](/help/mobile/administer-mobile-apps.md)**.

### Entità nel modello di contenuto {#entities-in-content-model}

Un&#39;entità è un&#39;istanza di un modello di contenuto. Un’entità viene esposta alla libreria lato client tramite l’API Content Services e consente a un’app nativa di accedere al contenuto in modo indipendente dal canale.

Se è presente un contenuto AEM, un’entità viene generata utilizzando un modello e l’origine del contenuto AEM. Ad esempio, un’entità pagina è un oggetto indipendente dal canale e dal layout generato da una pagina AEM e dal modello della pagina.

Le modifiche al contenuto di riferimento di un’entità determinano una modifica dell’entità. Se ad esempio si aggiorna una *cq:page*, verranno aggiornate anche tutte le entità basate su tale pagina.

Per creare entità personalizzate dai modelli, vedi **[Utilizzo delle entità](/help/mobile/spaces-and-entities.md)**.

>[!NOTE]
>
>Se il modello non corrisponde a un contenuto AEM esistente, ad esempio il cliente ha creato un modello, è disponibile un’interfaccia utente che consente al cliente di creare un’entità.
>

### Spazi nel modello di contenuto {#spaces-in-content-model}

Viene utilizzato uno spazio per organizzare le entità in modo da semplificarne l&#39;accesso. Uno spazio può contenere uno o più tipi di entità e può contenere sottocartelle.

Sul lato AEM, uno spazio è un modo conveniente per gestire le entità correlate. Può anche essere utilizzato per assegnare autorizzazioni di autorizzazione. L&#39;autorizzazione può essere concessa a uno spazio, che protegge le entità presenti in tale spazio.

*Ad esempio*,

Un utente dispone di tre classificazioni generali di entità. Una è solo per uso interno, un’altra è approvata per l’uso pubblico e ancora una terza è per le entità comuni utilizzate da molte app. Per semplificare la gestione, l&#39;utente crea tre spazi: *internal*, *public* (con contenuti sia in inglese che in francese) e *common* per gestire le entità appropriate come indicato di seguito:

* /content/entities/internal
* /content/entities/public/it
* /content/entities/public/fr
* /content/entities/common

Allo spazio viene fornito un endpoint di servizio in modo che la libreria client nativa possa richiedere un elenco dei contenuti di uno spazio. Questa &quot;voce&quot; viene restituita come oggetto JSON.

Consulta **[Spazi ed entità](/help/mobile/spaces-and-entities.md)** per la creazione e la pubblicazione di spazi.

>[!NOTE]
>
>Uno spazio può essere utilizzato da molte app e un&#39;app può utilizzare più spazi.

### Cartelle nel modello di contenuto {#folders-in-content-model}

Le cartelle consentono agli utenti di organizzare le entità in base alle esigenze e facilitano un controllo ACL più preciso. Gli spazi possono includere cartelle per organizzare ulteriormente il contenuto e le risorse dello spazio. Un utente può creare la propria gerarchia sotto uno spazio.

Per creare e gestire cartelle all&#39;interno di uno spazio, vedere **[Utilizzo delle cartelle in uno spazio](/help/mobile/spaces-and-entities.md)**.
