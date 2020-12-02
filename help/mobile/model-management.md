---
title: Panoramica sui modelli
seo-title: Panoramica sui modelli
description: 'null'
seo-description: 'null'
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---


# Panoramica dei modelli{#models-overview}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La gestione dei modelli prevede la creazione e la gestione di modelli allo scopo di associare a eventuali oggetti dati. Ogni modello includerà tutte le proprietà e le definizioni dei campi necessarie per facilitare la creazione e il rendering degli oggetti.

Gestione modelli prevede la creazione di **modelli**, **entità** e **spazi**. Il diagramma seguente illustra la relazione tra il contenuto AEM e i modelli.

![chlimage_1-81](assets/chlimage_1-81.png)

## Modello di contenuto {#the-content-model}

Un modello descrive il tipo di contenuto e indica quali informazioni saranno disponibili per l&#39;applicazione nativa. È una descrizione di ciò che costituisce un contenuto. Un modello di contenuto è la regola per la creazione di un contenuto. Il modello di contenuto include i dati disponibili, le risorse utilizzabili, la relazione tra risorse e dati, la relazione con altri modelli di contenuto e i metadati disponibili.

I modelli servono anche a trasformare il contenuto AEM esistente in oggetti che possono essere facilmente utilizzati dalle app mobili native.

Content Services fornirà alcuni modelli out-of-the-box per oggetti comuni come risorse, raccolte di risorse, pagine HTML, configurazioni di app e pagine indipendenti dai canali. Questi elementi saranno configurabili in modo da soddisfare specifiche esigenze dei clienti senza dover AEM sforzo di sviluppo.

L&#39;utente può creare modelli personalizzati. Questo consente la creazione di nuovi tipi di contenuto che non sono già gestiti da AEM. La creazione di un modello viene eseguita tramite un&#39;interfaccia utente che utilizza i tipi di base esistenti.

Il diagramma seguente illustra il modello di contenuto per  app AEM Mobile e come entità, cartelle e spazi vengono assegnati a un&#39;app.

![chlimage_1-82](assets/chlimage_1-82.png)

### I modelli {#the-models}

I modelli vengono utilizzati per determinare in che modo vengono create le entità. Definiscono ciò che è disponibile in un&#39;entità e come tali dati vengono generati dal contenuto AEM. Prima di iniziare a lavorare con Spazi, Cartelle ed Entità, è necessario avere familiarità con la creazione e la gestione di modelli.

>[!NOTE]
>
>Un modello esiste all&#39;esterno di un&#39;app in quanto più app possono utilizzarlo.


Vedere **[Modelli](/help/mobile/administer-mobile-apps.md)** per creare e gestire modelli nel dashboard e nella directory archivio.

### Entità nel modello di contenuto {#entities-in-content-model}

Un&#39;entità è un&#39;istanza di un modello di contenuto. Un&#39;entità viene esposta tramite Content Services API alla libreria lato client e fornisce un modo per un&#39;app nativa di accedere al contenuto in modo indipendente dal canale.

Nel caso del contenuto AEM esistente, un&#39;entità viene generata utilizzando un modello e l&#39;origine di contenuto AEM. Ad esempio, un&#39;entità pagina è un oggetto indipendente dal canale e dal layout generato da una pagina AEM e dal modello di pagina.

Le modifiche al contenuto di riferimento di un&#39;entità determineranno una modifica all&#39;entità. Ad esempio, se viene aggiornato un *cq:page*, verranno aggiornate anche tutte le entità basate su tale pagina.

Vedere **[Utilizzo di Entità](/help/mobile/spaces-and-entities.md)** per creare entità personalizzate dai modelli.

>[!NOTE]
>
>Se il modello non corrisponde a un contenuto AEM esistente, ad esempio il cliente ha creato un nuovo modello, sarà disponibile un&#39;interfaccia utente in modo che il cliente possa creare una nuova entità.


### Spazi nel modello di contenuto {#spaces-in-content-model}

Uno spazio viene utilizzato per organizzare le entità per un accesso facilitato. Uno spazio può contenere uno o più tipi di entità e può contenere sottocartelle.

Dal lato AEM, uno spazio è un modo conveniente per gestire le entità correlate. Può essere utilizzato anche per assegnare le autorizzazioni. È possibile autorizzare uno spazio per proteggere le entità che si trovano in tale spazio.

*Esempio*,

Un utente ha tre classificazioni generali di entità. Uno è solo per uso interno, un altro è approvato per uso pubblico e ancora un terzo è per le entità comuni che vengono utilizzate da molte app. Per semplificare la gestione, l&#39;utente crea tre spazi: *internal*, *public* (con contenuti sia inglesi che francesi) e *common* per la gestione delle entità appropriate come indicato di seguito:

* /content/entities/internal
* /content/entities/public/en
* /content/entities/public/fr
* /content/entities/common

Verrà fornito un punto finale del servizio allo spazio in modo che la libreria client nativa possa richiedere un elenco dei contenuti di uno spazio. Questo &quot;elenco&quot; verrà restituito come oggetto JSON.

Per creare e pubblicare spazi, consultate **[Spazi e entità](/help/mobile/spaces-and-entities.md)**.

>[!NOTE]
>
>Uno spazio può essere utilizzato da molte app e un&#39;app può utilizzare molti spazi.

### Cartelle nel modello di contenuto {#folders-in-content-model}

Le cartelle consentono agli utenti di organizzare le entità come richiesto e facilitano un controllo ACL più preciso. Gli spazi possono includere cartelle per organizzare ulteriormente il contenuto e le risorse dello spazio. Un utente può creare una propria gerarchia sotto uno spazio.

Vedere **[Utilizzo delle cartelle in uno spazio](/help/mobile/spaces-and-entities.md)** per creare e gestire le cartelle all&#39;interno di uno spazio.
