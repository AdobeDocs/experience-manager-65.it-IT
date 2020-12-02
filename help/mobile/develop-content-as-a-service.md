---
title: Distribuzione dei contenuti
seo-title: Distribuzione dei contenuti
description: 'null'
seo-description: 'null'
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 1%

---


# Distribuzione dei contenuti{#content-delivery}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Le app mobili dovrebbero essere in grado di utilizzare qualsiasi contenuto e tutto il contenuto in AEM in base alle esigenze per fornire l&#39;esperienza app di destinazione.

Ciò include l&#39;utilizzo di risorse, contenuto del sito, contenuto CaaS (over-the-air) e contenuto personalizzato che può avere una propria struttura.

>[!NOTE]
>
>**I contenuti over-the-Air** possono provenire da una delle funzionalità precedenti tramite gestori ContentSync. Può essere utilizzato per il pacchetto batch e la consegna tramite zip, nonché mantenere gli aggiornamenti o tali pacchetti.

I servizi Content Services forniscono tre tipi principali di materiale:

1. **Assets**
1. **Contenuto HTML con pacchetto (HTML/CSS/JS)**
1. **Contenuto indipendente dal canale**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

Le raccolte di risorse sono AEM costrutti che contengono riferimenti ad altre raccolte.

Una raccolta di risorse può essere esposta tramite Content Services. Una chiamata a una raccolta di risorse in una richiesta restituisce un oggetto che è un elenco delle risorse, inclusi i relativi URL. Le risorse sono accessibili tramite un URL. L&#39;URL viene fornito in un oggetto. Esempio:

* Un&#39;entità pagina restituisce JSON (oggetto pagina) che include un riferimento immagine. Il riferimento immagine è un URL utilizzato per ottenere il binario della risorsa per l’immagine.
* Una richiesta di un elenco di risorse in una cartella restituisce un JSON con dettagli su tutte le entità in tale cartella. Quell&#39;elenco è un oggetto. Il JSON dispone di riferimenti URL che vengono utilizzati per ottenere il binario della risorsa per ogni risorsa in quella cartella.

### Ottimizzazione risorse {#asset-optimization}

Un valore chiave di Content Services è la capacità di restituire le risorse ottimizzate per il dispositivo. Questo riduce le esigenze di archiviazione locale dei dispositivi e migliora le prestazioni delle app.

L&#39;ottimizzazione delle risorse sarà una funzione lato server, basata sulle informazioni fornite nella richiesta API. Laddove possibile, le rappresentazioni delle risorse dovrebbero essere memorizzate nella cache in modo che richieste simili non richiedano una nuova generazione della rappresentazione delle risorse.

### Flusso di lavoro risorse {#assets-workflow}

Il flusso di lavoro delle risorse è il seguente:

1. Riferimento risorse disponibile in AEM out-of-the-box
1. Crea entità di riferimento risorsa in base al modello
1. Modifica entità

   1. Scegli una risorsa o una raccolta di risorse
   1. Personalizzare il rendering JSON

Il diagramma seguente mostra il flusso di lavoro di riferimento delle **risorse**:

![chlimage_1-155](assets/chlimage_1-155.png)

### Gestione delle risorse {#managing-assets}

Content Services fornisce l&#39;accesso a AEM risorse gestite a cui potrebbero non essere presenti riferimenti tramite altri contenuti AEM.

#### Risorse gestite esistenti {#existing-managed-assets}

Un utente  AEM Sites e Assets esistente utilizza  AEM Assets per gestire tutto il materiale digitale per tutti i canali. Stanno sviluppando un&#39;app mobile nativa e devono utilizzare diverse risorse gestite da  AEM Assets. Ad esempio logo, immagini di sfondo, icone di pulsanti, ecc.

Attualmente questi sono distribuiti nell’archivio delle risorse. I file a cui l&#39;app deve fare riferimento sono:

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Accesso a entità risorsa CS {#accessing-cs-asset-entities}

Mettiamo da parte i passaggi per rendere la pagina disponibile tramite l’API per il momento (sarà coperta dalla descrizione dell’interfaccia utente AEM) e presupponiamo che sia stata completata. Le entità risorsa sono state create e aggiunte allo spazio &quot;appImages&quot;. Ulteriori cartelle sono state create nello spazio a scopo organizzativo. Pertanto, le entità delle risorse sono memorizzate nel JCR AEM come:

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/Grey_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### Ottenimento di un elenco di entità risorsa disponibili {#getting-a-list-of-available-asset-entities}

Gli sviluppatori di app possono ottenere un elenco delle risorse disponibili, recuperando le entità delle risorse. L&#39;endpoint spazio di Content Services può fornire tali informazioni tramite l&#39;SDK API del servizio Web.

Il risultato sarebbe un oggetto in formato JSON che fornirebbe un elenco delle risorse nella cartella &quot;icons&quot;.

![chlimage_1-156](assets/chlimage_1-156.png)

#### Ottenimento di un&#39;immagine {#getting-an-image}

Il JSON fornisce un URL per ogni immagine, generato da Content Services all&#39;immagine.

Per ottenere il binario per l&#39;immagine &quot;carrello&quot;, la libreria client viene utilizzata di nuovo.

## Contenuto HTML con pacchetto {#packaged-html-content}

Il contenuto HTML è necessario per i clienti che devono mantenere il layout del contenuto. Questo è utile per le applicazioni native che utilizzano un contenitore Web, come una visualizzazione Web Cordova, per visualizzare il contenuto.

AEM Content Services sarà in grado di fornire contenuto HTML all&#39;app mobile tramite l&#39;API. I clienti che desiderano esporre AEM contenuto come HTML creeranno un&#39;entità pagina HTML che punta all&#39;origine contenuto AEM.

Vengono considerate le seguenti opzioni:

* **File ZIP:** per avere la migliore possibilità di essere visualizzato correttamente sul dispositivo, tutto il materiale di riferimento della pagina (css, JavaScript, risorse, ecc.) - verrà incluso in un singolo file compresso con la risposta. I riferimenti nella pagina HTML verranno modificati per utilizzare un percorso relativo a tali file.
* **Streaming:** ottenere un manifesto dei file richiesti da AEM. Quindi utilizzate il manifesto per richiedere tutti i file (HTML, CSS, JS, ecc.) con richieste successive.

![chlimage_1-157](assets/chlimage_1-157.png)

## Contenuto indipendente dal canale {#channel-independent-content}

Il contenuto indipendente dal canale è un modo per esporre AEM costrutti di contenuto, come le pagine, senza preoccuparsi del layout, dei componenti o di altre informazioni specifiche del canale.

Queste entità di contenuto vengono generate utilizzando un modello di contenuto per tradurre le strutture di AEM in un formato JSON. I dati JSON risultanti contengono informazioni sui dati del contenuto, che vengono disaccoppiati dall&#39;archivio AEM. Ciò include la restituzione di metadati e AEM collegamenti di riferimento alle risorse, nonché le relazioni tra le strutture di contenuto, inclusa la gerarchia delle entità.

### Gestione del contenuto indipendente dal canale {#managing-channel-independent-content}

Il contenuto può essere immesso nell&#39;app in diversi modi.

1. GET i contenuti ZIPS tramite AEM Over-the-Air

   * I gestori di sincronizzazione dei contenuti possono aggiornare il pacchetto zip direttamente o chiamando i renderer di contenuti esistenti

      * Gestori piattaforma
      * Gestori AEMM
      * Gestori personalizzati

1. GET di contenuti direttamente tramite i renderer di contenuti

   * Renderer Sling predefiniti integrati
   *  AEM Mobile/Content Services Content Renderer
   * Rendering personalizzati

