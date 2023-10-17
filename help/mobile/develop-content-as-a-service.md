---
title: Consegna dei contenuti
description: Scopri come utilizzare tutti i contenuti in Adobe Experience Manager per fornire un’esperienza di app mirata.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 1%

---

# Consegna dei contenuti{#content-delivery}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Le app mobili devono essere in grado di utilizzare tutti i contenuti dell’AEM in base alle esigenze, per fornire un’esperienza di utilizzo dell’app mirata.

Ciò include l’utilizzo di risorse, contenuto del sito, contenuto CaaS (over-the-air) e contenuto personalizzato che può avere una propria struttura.

>[!NOTE]
>
>**Contenuti trasmessi via etere** può provenire da uno qualsiasi dei precedenti tramite gestori ContentSync. Può essere utilizzato per raggruppare il pacchetto e la consegna tramite zip e mantenere gli aggiornamenti per tali pacchetti.

I servizi di contenuti forniscono tre tipi principali di materiale:

1. **Risorse**
1. **Contenuto Packaged HTML (HTML/CSS/JS)**
1. **Contenuto indipendente dal canale**

![chlimage_1-154](assets/chlimage_1-154.png)

## Risorse {#assets}

Le raccolte di risorse sono costrutti AEM che contengono riferimenti ad altre raccolte.

Una raccolta di risorse può essere esposta tramite Content Services. Quando si richiama una raccolta di risorse in una richiesta, viene restituito un oggetto che è un elenco delle risorse, inclusi i relativi URL. Le risorse sono accessibili tramite un URL. L’URL viene fornito in un oggetto. Ad esempio:

* Un’entità pagina restituisce il JSON (oggetto pagina) che include un riferimento a un’immagine. Il riferimento immagine è un URL utilizzato per ottenere il binario della risorsa per l’immagine.
* Una richiesta per un elenco di risorse in una cartella restituisce il JSON con i dettagli di tutte le entità in tale cartella. Tale elenco è un oggetto. Il JSON dispone di riferimenti URL utilizzati per ottenere il binario della risorsa per ogni risorsa in quella cartella.

### Ottimizzazione risorse {#asset-optimization}

Un valore chiave di Content Services è la capacità di restituire le risorse ottimizzate per il dispositivo. Questo riduce le esigenze di archiviazione del dispositivo locale e migliora le prestazioni dell’app.

L’ottimizzazione delle risorse è una funzione lato server, basata sulle informazioni fornite nella richiesta API. Quando possibile, le rappresentazioni delle risorse devono essere memorizzate nella cache, in modo che richieste simili non richiedano la rigenerazione della rappresentazione delle risorse.

### Flusso di lavoro risorse {#assets-workflow}

Il flusso di lavoro delle risorse è il seguente:

1. Riferimento agli asset disponibile nell’AEM preconfigurato
1. Creare un’entità di riferimento risorsa in base al modello
1. Modifica entità

   1. Scegli una risorsa o una raccolta di risorse
   1. Personalizzare il rendering JSON

Il diagramma seguente mostra **Flusso di lavoro di riferimento risorse**:

![chlimage_1-155](assets/chlimage_1-155.png)

### Gestione delle risorse {#managing-assets}

Content Services fornisce l&#39;accesso alle risorse gestite dall&#39;AEM a cui non è possibile fare riferimento tramite altri contenuti AEM.

#### Risorse gestite esistenti {#existing-managed-assets}

Un utente di AEM Sites e Assets utilizza AEM Assets per gestire tutto il proprio materiale digitale per tutti i canali. Stanno sviluppando un’app mobile nativa e devono utilizzare diverse risorse gestite da AEM Assets. Ad esempio loghi, immagini di sfondo e icone dei pulsanti.

Attualmente queste sono distribuite nell’archivio delle risorse. I file a cui l’app deve fare riferimento sono i seguenti:

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/grey_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Accesso alle entità delle risorse CS {#accessing-cs-asset-entities}

Lasciamo da parte i passaggi del modo in cui la pagina viene resa disponibile tramite l’API per il momento (è coperta dalla descrizione dell’interfaccia utente dell’AEM) e supponiamo che sia stata eseguita. Le entità risorsa sono state create e aggiunte allo spazio &quot;appImages&quot;. Sono state create ulteriori cartelle nello spazio a scopo organizzativo. Pertanto, le entità delle attività sono memorizzate nel JCR dell’AEM come:

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### Ottenimento di un elenco di entità risorse disponibili {#getting-a-list-of-available-asset-entities}

Uno sviluppatore di app può ottenere un elenco delle risorse disponibili recuperando le entità delle risorse. L’endpoint dello spazio di Content Services può fornire tali informazioni tramite l’SDK dell’API del servizio web.

Il risultato sarebbe un oggetto in formato JSON che fornirebbe un elenco delle risorse nella cartella &quot;icons&quot;.

![chlimage_1-156](assets/chlimage_1-156.png)

#### Recupero di un’immagine {#getting-an-image}

Il JSON fornisce un URL per ogni immagine generata da Content Services per l’immagine.

Per ottenere il binario per l’immagine &quot;carrello&quot;, viene utilizzata di nuovo la libreria client.

## Contenuto Packaged HTML {#packaged-html-content}

Il contenuto HTML è necessario per i clienti che devono mantenere il layout del contenuto. Questa funzione è utile per le applicazioni native che utilizzano un contenitore Web, ad esempio una visualizzazione Web Cordova, per visualizzare il contenuto.

AEM Content Services fornisce contenuti HTML all’app mobile tramite l’API. I clienti che desiderano esporre contenuti AEM come HTML possono creare un’entità pagina HTML che punta all’origine di contenuto AEM.

Sono considerate le seguenti opzioni:

* **File ZIP:** Per avere la migliore possibilità di visualizzare correttamente sul dispositivo, i materiali di riferimento della pagina (css, JavaScript, risorse e così via) sono inclusi in un singolo file compresso con la risposta. I riferimenti nella pagina HTML possono essere regolati in modo da utilizzare un percorso relativo per questi file.
* **Streaming:** Recupero di un manifesto dei file richiesti da AEM. Quindi utilizza tale manifesto per richiedere tutti i file (HTML, CSS, JS e così via) con le richieste successive.

![chlimage_1-157](assets/chlimage_1-157.png)

## Contenuto indipendente dal canale {#channel-independent-content}

I contenuti indipendenti dal canale sono un modo per esporre i costrutti dei contenuti AEM, come le pagine, senza preoccuparsi del layout, dei componenti o di altre informazioni specifiche per il canale.

Queste entità di contenuto vengono generate utilizzando un modello di contenuto per tradurre le strutture dell’AEM in formato JSON. I dati JSON risultanti contengono informazioni sui dati del contenuto che sono separati dall’archivio AEM. Ciò include la restituzione di metadati e collegamenti di riferimento AEM alle risorse e le relazioni tra le strutture di contenuto, inclusa la gerarchia di entità.

### Gestione di contenuti indipendenti dal canale {#managing-channel-independent-content}

Il contenuto può arrivare all’app in diversi modi.

1. Contenuto GET ZIPS tramite AEM Over-the-Air

   * I gestori di sincronizzazione del contenuto possono aggiornare il pacchetto zip direttamente o chiamando i renderer di contenuto esistenti

      * Gestori di piattaforma
      * Gestori AEM
      * Gestori personalizzati

1. GET il contenuto direttamente tramite i renderer di contenuto

   * Rendering Sling predefiniti preconfigurati
   * AEM Mobile/Content Services - Rendering contenuti
   * Rendering personalizzati
