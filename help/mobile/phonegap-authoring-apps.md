---
title: Creazione di applicazioni mobili
seo-title: Creazione di applicazioni mobili
description: ' AEM Mobile Dashboard consente di creare, creare e distribuire l’applicazione mobile, creare, eliminare e modificare i metadati dell’applicazione. Segui questa pagina per saperne di più.'
seo-description: ' AEM Mobile Dashboard consente di creare, creare e distribuire l’applicazione mobile, creare, eliminare e modificare i metadati dell’applicazione. Segui questa pagina per saperne di più.'
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---


# Creazione di applicazioni mobili{#authoring-mobile-applications}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

 AEM Mobile Dashboard consente di creare, creare e distribuire l&#39;applicazione mobile, creare, eliminare e modificare i metadati dell&#39;applicazione. Una volta che l&#39;applicazione è live, puoi analizzare l&#39;analisi delle applicazioni, compresi il ciclo di vita e le metriche di utilizzo, per migliorare la conversione dei clienti e la fedeltà al marchio.

Per creare l&#39;applicazione AEM Mobile , vedere la pagina [Creazione di applicazioni mobili](/help/mobile/building-app-mobile-phonegap.md).

Per configurare l&#39;ambiente e iniziare, vedere [AEM di amministrazione per utilizzare AEM PhoneGap Enterprise](/help/mobile/administer-phonegap.md).

## Catalogo  app AEM Mobile {#the-aem-mobile-apps-catalog}

Il [ AEM Mobile Apps Catalog](http://localhost:4502/aem/apps.html/content/phonegap) visualizza tutta l&#39;app mobile gestita in AEM.

Considerate questo catalogo come la &quot;pagina di destinazione&quot; di  AEM Mobile, in cui gli amministratori possono avviare una nuova applicazione AEM Mobile  creando un modello basato su di esso, oppure caricando un&#39;app esistente già avviata da uno sviluppatore di dispositivi mobili.

Per accedere alla pagina di destinazione del catalogo delle app, effettuate le seguenti operazioni:

1. Passare a **Navigazione** e scegliere **Mobile**.

1. Scegliete **App** per aprire il catalogo delle app.

![ AEM Mobile Apps Catalog](assets/chlimage_1-135.png)

## Il  AEM Mobile App Dashboard {#the-aem-mobile-app-dashboard}

Quando si seleziona un&#39;app AEM Mobile  dal catalogo, viene visualizzata la relativa dashboard. Qui puoi gestire l&#39;applicazione, visualizzare le statistiche, creare, distribuire e gestire il contenuto dell&#39;app mobile.

Per visualizzare o modificare i dettagli, potete espanderli in ciascuna sezione del  AEM Mobile Dashboard facendo clic su &#39;...&#39; nell&#39;angolo in basso a destra.

![ AEM Mobile Applications Command Center](assets/chlimage_1-136.png)

### Gestisci sezione app {#the-manage-app-tile}

La sezione Gestione app visualizza l&#39;icona dell&#39;applicazione, il nome, la descrizione, le piattaforme supportate, la pagina principale per gli aggiornamenti URL e le informazioni sulla versione. È possibile esaminare questa sezione per modificare e gestire la configurazione dell&#39;applicazione PhoneGap (config.xml) e preparare l&#39;applicazione per l&#39;invio ai diversi store applicazioni per la distribuzione.

Fare clic [qui](/help/mobile/phonegap-app-details-tile.md) per ulteriori informazioni.

![chlimage_1-137](assets/chlimage_1-137.png)

### Gestisci sezione contenuto pagina {#the-manage-page-content-tile}

Il contenuto può essere creato, aggiornato ed eliminato in  AEM Mobile nello stesso modo in cui si esegue  AEM Sites. La **Gestisci sezione contenuto pagina** visualizza il numero di pagine di contenuto gestito e l&#39;ultima modifica. Per approfondire i contenuti per creare, copiare, spostare, eliminare e aggiornare le pagine, fate clic su ciascun record nella sezione. Una volta aggiornato il contenuto, potete inviare un aggiornamento dei contenuti ai clienti tramite la sezione **Gestisci pacchetti di contenuti.**

![Sezione contenuto](assets/chlimage_1-138.png)

### Sezione Gestisci pacchetti di contenuti {#the-manage-content-packages-tile}

Dopo aver aggiunto o modificato il contenuto tramite la sezione Gestisci contenuto pagina, potete inviare tali modifiche ai clienti con un aggiornamento della versione del contenuto.

Content Package (Pacchetto contenuti) consente a AEM App Author di gestire il contenuto della pagina in AEM e al team di sviluppo di apportare modifiche all&#39;applicazione PhoneGap Shell (ovvero all&#39;infrastruttura o all&#39;ambito dell&#39;app) e inviare tali modifiche ai clienti in modo rapido e senza dover coinvolgere uno sviluppatore per reinviare i diversi store per la distribuzione.

Pacchetto di contenuti crea un file ZIP, considerato pacchetto di rilascio dei contenuti, per ciascun aggiornamento. Questi pacchetti contengono risorse html e pagine html che vengono generate durante il rendering dell&#39;app ed è sufficientemente intelligente da creare pacchetti solo per i file che sono stati modificati dall&#39;ultimo aggiornamento.

La colonna Gestisci sezione pacchetto contenuto **Tipo** mostrerà &#39;App&#39; per indicare il contenuto di Shell applicazione, ad esempio il framework o l&#39;infrastruttura dell&#39;app gestita da uno sviluppatore oppure &#39;Content&#39; che rappresenta il contenuto della pagina gestito dall&#39;autore del contenuto.

Il contenuto può essere rappresentato come una lingua o come una parte particolare dell&#39;app in cui più pacchetti di rilascio del contenuto vengono utilizzati dall&#39;app. La scelta della modalità di bundle dei contenuti è stata progettata per essere flessibile e all&#39;altezza di come si desidera gestire i contenuti per l&#39;applicazione.

La colonna **Modificato** indica quando le pagine sono state modificate più di recente.

La colonna **Staged** mostra quando è stato creato l&#39;ultimo aggiornamento del contenuto. Per creare un nuovo aggiornamento del contenuto e mettere in scena le modifiche, aprite qualsiasi record nella sezione e create un nuovo aggiornamento.

La colonna **Published** (Pubblicato) mostra quando è stato pubblicato l&#39;ultimo aggiornamento del contenuto e reso disponibile dai clienti per il consumo. Per pubblicare il contenuto, dovete prima eseguire il passaggio del contenuto e quindi pubblicare l&#39;aggiornamento estraendolo in questa sezione e pubblicandolo dalla console Dettagli rilascio contenuto.

![Pacchetto ](assets/chlimage_1-139.png) ![TileContentSync della versione del contenuto per la shell dell&#39;app](do-not-localize/chlimage_1-5.png)

Questa icona rappresenta un pacchetto di rilascio del contenuto per la shell dell&#39;app

![](do-not-localize/chlimage_1-6.png)

Queste icone rappresentano un pacchetto di rilascio del contenuto per il contenuto dell&#39;app

### Tile di PhoneGap Build {#the-phonegap-build-tile}

La **PhoneGap Build Tile** si collega a [https://build.phonegap.com](https://build.phonegap.com) per creare e ospitare i buids remoti. Una volta creata, la build viene resa disponibile come download o direttamente sul dispositivo tramite un codice QR.

In alternativa, è possibile scaricare l&#39;origine del dispositivo per creare localmente tramite l&#39;interfaccia CLI di [PhoneGap](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html).

![PhoneGap Build](assets/chlimage_1-140.png)

### Sezione Metriche {#the-metrics-tile}

>[!CAUTION]
>
>La sezione Metriche viene visualizzata solo dopo la configurazione del servizio cloud.
>
>Per ulteriori informazioni, vedere [Configurare il Cloud Service  Mobile Services](/help/mobile/configure-adobe-mobile-cloud-service.md).

 AEM Mobile si integra con  Adobe Analytics tramite [ Adobe SDK di Mobile Services](https://www.adobe.com/ca/solutions/digital-marketing/mobile-services/app-sdk.html) (AMS).

Il Centro di controllo **Metrics Tile** visualizza l&#39;analisi di riepilogo estratta da AMS per l&#39;applicazione. Per approfondire il dashboard di analisi, fai clic su &#39;...&#39; in basso a destra.

![Sezione Metriche](assets/chlimage_1-141.png)

### La sezione Gestisci contenuto entità {#the-manage-entity-content-tile}

La sezione Gestisci contenuto entità consente di aggiungere e gestire le definizioni delle app. Le definizioni delle app sono un modo per identificare gli spazi (e altre configurazioni) appropriati per l&#39;app. In questo modo è possibile aggiungere un nuovo spazio senza dover ricompilare l&#39;app. La definizione dell&#39;app viene aggiornata e includerà le informazioni per eventuali nuovi spazi.

Fai clic [qui](/help/mobile/phonegap-app-definitions.md) per creare e gestire le definizioni delle app.

Per approfondire il dashboard di gestione del contenuto dell&#39;entità, fai clic su &#39;...&#39; in basso a destra.

![chlimage_1-142](assets/chlimage_1-142.png)

#### Risorse aggiuntive {#additional-resources}

Per informazioni su ruoli e responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Sviluppo per  Adobe PhoneGap Enterprise con AEM](/help/mobile/developing-in-phonegap.md)
* [Amministrazione di contenuti per  Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

